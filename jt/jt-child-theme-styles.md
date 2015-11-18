# Loading parent styles for child themes

In the past week, an interesting discussion has started on how best to handle stylesheets in child themes.  The discussion has centered around the best method for loading a parent theme stylesheet via a child theme.  Morten Rand-Hendriksen kicked off the discussion in his post [Challenges with the new method for inheriting parent styles in WordPress child themes](http://mor10.com/challenges-new-method-inheriting-parent-styles-wordpress-child-themes).

Because I've been doing parent/child themes since it was possible to do so in WordPress, I have some experience in this area.  Frankly, there's not much of a problem from my perspective.  I actually have a simple fix that I use at [Theme Hybrid](http://themehybrid.com), which I'll get to in a bit.

Here's some extra-curricular reading if you want to catch up more on the topic going around:

* [Codex: How to create a child theme](http://codex.wordpress.org/Child_Themes#How_to_Create_a_Child_Theme)
* [Handbook: Inheriting styles in child themes](https://developer.wordpress.org/themes/advanced-topics/child-themes/#4-inherit-styles)
* [_s Theme: Load parent styles when child theme is activated](https://github.com/Automattic/_s/pull/638)

## Traditional method of loading styles

In the past few years, the widely-promoted technique for loading a parent theme stylesheet when creating a child theme has been the `@import` method.  It's pretty simple to do because it only requires a user to know one line of CSS as shown in the following code snippet.

	@import url( '../parent-theme-folder/style.css' );

Most developers will agree that we should try to avoid using `@import` for a number of reasons.  It loads slower than using `<link>` and doesn't necessarily play well with plugins concatenating styles.

The other side of that is that users often screw this part up.  Here's some of the issues I've seen with this method:

* Users can't figure out the parent theme folder name.
* Users changed the parent theme folder name.
* Users incorrectly typed in the code.

It's simple because it only has users messing around with CSS.  They're unlikely to bring their entire site down with incorrect code.  However, it's not a perfect system.

## The "new" method of loading styles

I don't really consider this new, per say.  Many theme authors have taught this method over the years.  However, it is the newer practice promoted on WordPress.org.  This method promotes good dev practice by not using `@import`.  Instead, it uses PHP to load the styles via the child theme's `functions.php` file as shown in the following code.

	add_action( 'wp_enqueue_scripts', 'my_parent_theme_css' );

	function my_parent_theme_css() {
		wp_enqueue_style( 'parent-style', get_template_directory_uri() . '/style.css' );
		wp_enqueue_style( 'child-style', get_stylesheet_uri(), array( 'parent-style' ) );
	}

There are some variations on that as well.  The basic idea is to more appropriately add the styles to `<head>` by using core WordPress functions.

The major problem with this method is that we're putting users (often first-time users) into the `functions.php` file, which can be a dangerous place.  One mistake here and you'll definitely bring your site down.  At least the `@import` method was a bit nicer about that.

The problems I see with above are numerous:

* Forces average users into `functions.php`.
* Doesn't take into account other styles that a parent theme uses.
* Makes the child style a dependent of the parent style (this can be removed with third parameter).
* Makes too many assumptions about what the parent theme is doing.

## My method of loading styles

Honestly, I didn't think my method was all that unique.  I figured everyone was doing something like this or similar these days.  *So, what's this fancy solution?*  

Load all the styles via the parent theme.

All of the other solutions propose loading styles via the child theme.  That's working toward the solution from the wrong direction.

Why bother making users figure out how to load styles at all?  As theme authors, we can go ahead and take care of this without having to worry our users with all this stuff.  The following code is how I've been doing it for a long while now.

	add_action( 'wp_enqueue_scripts', 'my_enqueue_styles' );

	function my_enqueue_styles() {

		/* If using a child theme, auto-load the parent theme style. */
		if ( is_child_theme() ) {
			wp_enqueue_style( 'parent-style', trailingslashit( get_template_directory_uri() ) . 'style.css' );
		}

		/* Always load active theme's style.css. */
		wp_enqueue_style( 'style', get_stylesheet_uri() );
	}

This method carries with it none of the issues of the other methods.  It makes your theme even friendlier to users who want to create child themes and gets rid of that nasty `@import`.  That's a win-win in my book.

The one potential issue is when users do not want the parent theme stylesheet to load.  For that particular use case, you simply teach them how to do it via `functions.php`.  Since we almost always want to load the parent theme styles, I consider this scenario an exception to the rule and an acceptable situation to have the user fiddling in the child theme's `functions.php` file.  Here's the code to do it:

	add_action( 'wp_enqueue_scripts', 'my_dequeue_styles', 11 );

	function my_dequeue_styles() {
		wp_dequeue_style( 'parent-style' );
	}

That's all there is to it.  Now, let's all make our themes just a little bit child theme friendlier.