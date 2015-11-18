# Post relationships: Parent-to-child

WordPress supports very little in the way of post relationships.  The only one it supports out of the box is a one-to-one relationship from parent-to-child.  One of the questions that I see once in a while is how to make a post from one post type a child of a post from another post type.

A user on my support forums at [Theme Hybrid](http://themehybrid.com) had an interesting project he was building.  Here's an extremely general outlook at his setup.

* "Neighborhood" custom post type.
* "Place" post type for individual places within a neighborhood.
* Both post types are flat (non-hierarchical).
* Each place needed to be assigned to a specific neighborhood.

Because this was an interesting project with such a simple solution, I thought I'd share it with everyone.

## How to assign a parent post

I'm going to assume you're advanced enough to know how to build a plugin as well as understand the inner-workings of post types.  If not, I recommend reading my [tutorial on post types](http://justintadlock.com/archives/2010/04/29/custom-post-types-in-wordpress) for WordPress.

For this project, you'll need two non-hierarchical post types named `neighborhood` and `place`.  Now, for the fun part.  All you need to do is add the following code to your plugin's admin files.

	/* Hook meta box to just the 'place' post type. */
	add_action( 'add_meta_boxes_place', 'my_add_meta_boxes' );

	/* Creates the meta box. */
	function my_add_meta_boxes( $post ) {

		add_meta_box(
			'my-place-parent',
			__( 'Neighborhood', 'example-textdomain' ),
			'my_place_parent_meta_box',
			$post->post_type,
			'side',
			'core'
		);
	}

	/* Displays the meta box. */
	function my_place_parent_meta_box( $post ) {
	
		$parents = get_posts(
			array(
				'post_type'   => 'neighborhood', 
				'orderby'     => 'title', 
				'order'       => 'ASC', 
				'numberposts' => -1 
			)
		);
	
		if ( !empty( $parents ) ) {
	
			echo '<select name="parent_id" class="widefat">'; // !Important! Don't change the 'parent_id' name attribute.
	
			foreach ( $parents as $parent ) {
				printf( '<option value="%s"%s>%s</option>', esc_attr( $parent->ID ), selected( $parent->ID, $post->post_parent, false ), esc_html( $parent->post_title ) );
			}
	
			echo '</select>';
		}
	}

That's all there is to it.  You will, of course, want to alter the post type names to reference your own post types.

Here's a quick screenshot of the admin after applying the above code.

<img src="http://justintadlock.com/blog/wp-content/uploads/2013/10/post-type-parent-child.jpg" alt="Parent-to-child post relationship" width="779" height="434" class="aligncenter size-full wp-image-5229" />

## The hard part

So, the next question becomes, "How do I set up a hierarchical permalink structure for this?"  I'd rather have hot pokers thrust into my eyeballs than try to explain the WordPress rewrite API.  Ozh did a heck of a job writing that chapter in our [Plugin Dev Book](http://justintadlock.com/plugindevbook) if you're interested in diving into that sort of thing.

A lot of that depends on your custom setup anyway, so I'll leave that tutorial for another day.

## Other post relationships

Sure, this is cool, but it's also limited.  With your thinking cap on and post meta, you can do some pretty neat stuff outside of parent-to-child relationships.  It's not that tough for simple stuff, but for more complex relationships, you'll need to look at other solutions.

Post relationships are [potentially on the roadmap](http://make.wordpress.org/core/2013/07/28/potential-roadmap-for-taxonomy-meta-and-post-relationships/), but don't count on that being available soon.  Until then, I highly recommend the [Posts 2 Posts plugin](http://wordpress.org/plugins/posts-to-posts/).