# WordPress term meta

As we gear up for the release of WordPress version 4.4, many developers are planning some cool features that they've been waiting for years to implement.  These features revolve around term metadata.

The [original Trac ticket](https://core.trac.wordpress.org/ticket/10142) is over 6 years old.  A potential roadmap was [outlined by Andrew Nacin](https://make.wordpress.org/core/2013/07/28/potential-roadmap-for-taxonomy-meta-and-post-relationships/) a little over 2 years ago on the changes that would need to happen to get term meta in core WordPress.  Even if/when those changes happened, it didn't guarantee the inclusion of term meta.

Fortunately, this long sought-after developer feature was green-lighted for WordPress 4.4.

And, it's awesome.

## What is term meta?

Terms are individual objects within a taxonomy.  For example, the category taxonomy can have many categories (i.e., terms).

Meta (short for "metadata") is simply additional data that can be tied to an object.  This data can pretty much be anything.

Term meta, therefore, is additional data about specific taxonomy terms.

WordPress has long allowed for meta on other types of objects, such as:

* Posts
* Comments
* Users

If you've used WordPress, you've used metadata in some way, even if you didn't know it.  Metadata is actually pretty important because it allows plugins (and even core itself) to add extra data to the various objects that's not accounted for in the main table.

A good example of this is featured images in core.  Core stores the image ID as metadata because there's no field for the image ID in the posts table.  So, metadata to the rescue!

## Example uses of term meta

This is just an extremely small sampling of ideas:

* Term images.
* Storing the color hex code (e.g., `#000000`) to assign a color.
* Storing the document title via an SEO plugin.
* Category templates that can be re-used (like page templates).
* Attach an icon to a term.
* Theme sidebar position.
* Privatize posts that are in a specific category in a membership plugin.

One of my favorite [quotes about term meta](https://core.trac.wordpress.org/ticket/10142#comment:129) was written by John James Jacoby.

> Without term-meta, it's impossible to describe a tag or category beyond it's literal description. Terms are crippled without metadata, and are infinitely powerful with it.

I couldn't have said it better myself.

## Terms are not posts

Before moving forward, I want to touch on something that's been at the heart of the discussion of whether term meta even belongs in core at all.

Terms are not posts.

If you're building terms with vast amounts of metadata, particularly things that are maybe even handled better by posts, you might need to reconsider the architecture of your plugin.  Sure, the API allows for easy relationships, but if that's the only reason you're using a taxonomy instead of a custom post type, I'd urge you to consider the possibility of just building a post-to-post relationship (not that hard).

## How to use term meta

If you're a developer and have ever used post, comment, or user meta, you're pretty much already familiar with the foundations of term meta.  The biggest things you need to know are the new meta wrapper functions for terms:

* `add_term_meta()`
* `update_term_meta()`
* `delete_term_meta()`
* `get_term_meta()`

They work just like their `*_post|comment|user_meta()` siblings.  I don't think it's worth covering these in great detail.

Instead, I'm going to walk you through building a simple plugin using term meta.  What this plugin will do is allow users to assign a color to a category.  This can be useful for all sorts of things.  One thing that immediately comes to mind is designing a news theme and having a specific color associated with each category, which is typical of many news publications.

## Registering meta

The first step is to register our meta with the `register_meta()` function.  We'll name our custom meta key `color`.

	add_action( 'init', 'jt_register_meta' );

	function jt_register_meta() {
	
		register_meta( 'term', 'color', 'jt_sanitize_hex' );
	}

Note that we added a sanitize callback function for when meta is saved.  So, let's go ahead and add the code for that.  What the function is going to do is simply make sure that we have a valid color hex code.

	function jt_sanitize_hex( $color ) {
	
		$color = ltrim( $color, '#' );
	
		return preg_match( '/([A-Fa-f0-9]{3}){1,2}$/', $color ) ? $color : '';
	}

## Getting term meta

In order to get the stored term color, we use the `get_term_meta()` function like so:

	$color = get_term_meta( $term_id, 'color', true );

For the purposes of the plugin we're building, let's create a wrapper function that can return the color with or without the preceding `#` mark.

	function jt_get_term_color( $term_id, $hash = false ) {

		$color = get_term_meta( $term_id, 'color', true );
		$color = jt_sanitize_hex( $color );
	
		return $hash && $color ? "#{$color}" : $color;
	}

## Adding form fields

<img src="http://themehybrid.com/blog/wp-content/uploads/2015/11/term-color-field.png" alt="Category color field" width="869" height="554" class="aligncenter size-full wp-image-7323" />

Up to this point, everything we've done is not much different than post meta, for example.  Now, things will get a bit different.

If you've never added custom form fields to one of the taxonomy admin screens, there are two hooks you need to know about:

* `{$taxonomy}_add_form_fields` - Hook for adding fields to the "new term" form.
* `{$taxonomy}_edit_form_fields` - Hook for adding fields to the "edit term" form.

There's actually several hooks available if you dig into `wp-admin/edit-tags.php` and `wp-admin/edit-tag-form.php`.  I highly encourage scanning those files for calls to `do_action()` and finding the most appropriate hook for your use case.

One of the biggest things to note is that the add new term and edit term forms have different HTML markup.  This means that you need two separate callback functions for handling output of the fields.

For the add new form, we'll use the following code:

	add_action( 'category_add_form_fields', 'ccp_new_term_color_field' );
	
	function ccp_new_term_color_field() {
	
		wp_nonce_field( basename( __FILE__ ), 'jt_term_color_nonce' ); ?>
	
		<div class="form-field jt-term-color-wrap">
			<label for="jt-term-color"><?php _e( 'Color', 'jt' ); ?></label>
			<input type="text" name="jt_term_color" id="jt-term-color" value="" class="jt-color-field" data-default-color="#ffffff" />
		</div>
	<?php }

For the edit form, we'll use this code:
	
	add_action( 'category_edit_form_fields', 'ccp_edit_term_color_field' );
	
	function ccp_edit_term_color_field( $term ) {
	
		$default = '#ffffff';
		$color   = jt_get_term_color( $term->term_id, true );
	
		if ( ! $color )
			$color = $default; ?>
	
		<tr class="form-field jt-term-color-wrap">
			<th scope="row"><label for="description"><?php _e( 'Color', 'jt' ); ?></label></th>
			<td>
				<?php wp_nonce_field( basename( __FILE__ ), 'jt_term_color_nonce' ); ?>
				<input type="text" name="jt_term_color" id="jt-term-color" value="<?php echo esc_attr( $color ); ?>" class="jt-color-field" data-default-color="<?php echo esc_attr( $default ); ?>" />
			</td>
		</tr>
	<?php }

What we've done is add a basic text input to both forms for the color.  Remember, we're only adding this for the `category` taxonomy.  So, take note that the `category` part of the hooks is related specifically to that taxonomy.

## Saving term meta

In order to save the fields we added, we need to hook into `create_{$taxonomy}` (new term form) and `edit_{$taxonomy}` (edit term form).  Fortunately, we can use the same callback function with this and just check that our field was posted.

Again, take note that the `category` part refers specifically to the name of the taxonomy.

	add_action( 'edit_category',   'jt_save_term_color' );
	add_action( 'create_category', 'jt_save_term_color' );
	
	function jt_save_term_color( $term_id ) {
	
		if ( ! isset( $_POST['jt_term_color_nonce'] ) || ! wp_verify_nonce( $_POST['jt_term_color_nonce'], basename( __FILE__ ) ) )
			return $post_id;
	
		$old_color = jt_get_term_color( $term_id );
		$new_color = isset( $_POST['jt_term_color'] ) ? jt_sanitize_hex( $_POST['jt_term_color'] ) : '';
	
		if ( $old_color && '' === $new_color )
			delete_term_meta( $term_id, 'color' );
	
		else if ( $old_color !== $new_color )
			update_term_meta( $term_id, 'color', $new_color );
	}

That's pretty much it for handling the adding of custom form fields and saving the data.  We'll add a color picker in just a bit to make it look a bit prettier.

## Adding a term meta column

<img src="http://themehybrid.com/blog/wp-content/uploads/2015/11/term-color-column.png" alt="Category color column" width="844" height="386" class="aligncenter size-full wp-image-7324" />

On the taxonomy management page, you might want to add a custom column to output your metadata.  One thing to keep in mind is that the list table for taxonomies is kind of small, so too many columns can get unruly.

The first step is to let WordPress know about our custom column:

	add_filter( 'manage_edit-category_columns', 'jt_edit_term_columns' );
	
	function jt_edit_term_columns( $columns ) {
	
		$columns['color'] = __( 'Color', 'jt' );
	
		return $columns;
	}

Then, we need to handle the output for the column:

	add_filter( 'manage_category_custom_column', 'jt_manage_term_custom_column', 10, 3 );
	
	function jt_manage_term_custom_column( $out, $column, $term_id ) {
	
		if ( 'color' === $column ) {
	
			$color = jt_get_term_color( $term_id, true );
	
			if ( ! $color )
				$color = '#ffffff';
	
			$out = sprintf( '<span class="color-block" style="background:%s;">&nbsp;</span>', esc_attr( $color ) );
		}
	
		return $out;
	}

## Making things look pretty

We need a color picker instead of forcing users to manually type hex codes.  And, we need to make our color column nicer.

For that, we'll enqueue the `wp-color-picker` script and style while adding a little bit of custom JavaScript and CSS.

	add_action( 'admin_enqueue_scripts', 'jt_admin_enqueue_scripts' );
	
	function jt_admin_enqueue_scripts( $hook_suffix ) {
	
		if ( 'edit-tags.php' !== $hook_suffix || 'category' !== get_current_screen()->taxonomy )
			return;
	
		wp_enqueue_style( 'wp-color-picker' );
		wp_enqueue_script( 'wp-color-picker' );
	
		add_action( 'admin_head',   'jt_term_colors_print_styles' );
		add_action( 'admin_footer', 'jt_term_colors_print_scripts' );
	}
	
	function jt_term_colors_print_styles() { ?>
	
		<style type="text/css">
			.column-color { width: 50px; }
			.column-color .color-block { display: inline-block; width: 28px; height: 28px; border: 1px solid #ddd; }
		</style>
	<?php }
	
	function jt_term_colors_print_scripts() { ?>
	
		<script type="text/javascript">
			jQuery( document ).ready( function( $ ) {
				$( '.jt-color-field' ).wpColorPicker();
			} );
		</script>
	<?php }

## Only the beginning

This tutorial is just a small sampling of using the new term meta feature in WordPress 4.4.  There are other developer-features related to this that I encourage you to dig into.

Feel free to post any tutorial ideas in the comments or just share what you'd like to do with the new feature.