# Register multiple default backgrounds

One of the awesome things WordPress theme authors can do is register multiple default header images.  This allows their theme users to pick-and-choose from images that have been specifically optimized for the theme.  Unfortunately, I can't say the same thing about [custom backgrounds](http://codex.wordpress.org/Custom_Backgrounds).  If you want to add a default background to your theme, you're only allowed one image.

There is a WordPress [Trac ticket](http://core.trac.wordpress.org/ticket/18623) for this issue, but it seems to have gone stale with no movement for the past 15 months.

I've never needed that particular feature until now.  I'm building a super-awesome new theme for [Theme Hybrid](http://themehybrid.com) in which I'm designing multiple default header images.  But, I also want to add multiple default background images to go along with them.

Since there's no WordPress way to do this, I needed to build something that would pass the WordPress.org theme review guidelines.  In particular, I needed to meet the guideline for [theme features](http://codex.wordpress.org/Theme_Review#Theme_Features), which states that you must use the core implementation of a feature if you choose to use it.  

I decided to extend WordPress' custom background feature.  Follow along; I'll show you how to do it.

## The goal

This method is simply going to utilize the WordPress theme customizer.  I'm not too interested in doing this on the "Custom Background" screen in the admin, so I don't know how feasible that is.  The following is a screenshot of what we're building.

<img src="http://justintadlock.com/blog/wp-content/uploads/2013/10/default-backgrounds.png" alt="Multiple default backgrounds" width="700" height="641" class="aligncenter size-full wp-image-5240" />

## Extending the background image customize control

I'll assume from this point forward that you're already utilizing the `custom-background` feature in your theme.  You kind of need that for any of this to work.

To keep things simple and not have to do a lot of work, I created a class that extends the WordPress `WP_Customize_Background_Image_Control` class.  To use this class, create a file called `customize-control-background-image.php` in your theme add the following code to it.

I also created a [GitHub Gist](https://gist.github.com/justintadlock/6969375) for this class if you want to use it.

	<?php
	/**
	 * Extends the WordPress background image customize control class, which allows a theme to register
	 * multiple default backgrounds for the user to choose from.  To use this, the theme author 
	 * should remove the 'background_image' control and add this control in its place.
	 *
	 * @since     0.1.0
	 * @author    Justin Tadlock <justin@justintadlock.com>
	 * @copyright Copyright (c) 2013, Justin Tadlock
	 * @link      http://justintadlock.com/archives/2013/10/13/registering-multiple-default-backgrounds
	 * @license   http://www.gnu.org/licenses/old-licenses/gpl-2.0.html
	 */

	class JT_Customize_Control_Background_Image extends WP_Customize_Background_Image_Control {

		/**
		 * Array of default backgrounds.
		 *
		 * @since  0.1.0
		 * @access public
		 * @var    array
		 */
		public $jt_default_backgrounds = array();

		/**
		 * Set up our control.
		 *
		 * @since  0.1.0
		 * @access public
		 * @param  object  $manager
		 * @return void
		 */
		public function __construct( $manager ) {

			/* Let WP handle this. */
			parent::__construct( $manager );

			/* Allow themes to register custom backgrounds. */
			$this->jt_default_backgrounds = apply_filters( 'jt_default_backgrounds', $this->jt_default_backgrounds );

			/* WordPress will only output the 'default' tab if there's a default image. Make sure it gets added. */
			if ( !$this->setting->default && !empty( $this->jt_default_backgrounds ) )
				$this->add_tab( 'default', __( 'Default', 'jt' ), array( $this, 'tab_default_background' ) );
		}

		/**
		 * Displays the 'default' tab for selecting a background image.  This method plays nicely with the 
		 * 'default-image' argument for 'custom-background' as well as our custom backgrounds.
		 *
		 * @since  0.1.0
		 * @access public
		 * @return void
		 */
		public function tab_default_background() {

			/* If the theme added a 'default-image', make sure to output it. */
			if ( $this->setting->default )
				$this->print_tab_image( $this->setting->default );

			/* Check if the theme added an array of default backgrounds. */
			if ( !empty( $this->jt_default_backgrounds ) ) {

				/* Get the template and stylesheet directory URIs. */
				$template   = get_template_directory_uri();
				$stylesheet = get_stylesheet_directory_uri();

				/* Loop through the backgrounds and print them. */
				foreach ( $this->jt_default_backgrounds as $background ) {

					/* If no thumbnail was given, use the original. */
					if ( !isset( $background['thumbnail_url'] ) )
						$background['thumbnail_url'] = $background['url'];

					/* Use '%s' for parent themes and '%2$s' for child themes. */
					$url       = sprintf( $background['url'],           $template, $stylesheet );
					$thumb_url = sprintf( $background['thumbnail_url'], $template, $stylesheet );

					/* Print the image. */
					$this->print_tab_image( $url, $thumb_url );
				}
			}
		}
	}

	?>

## Customizing the customizer

The next thing we need to do is remove WordPress' background image control from the theme customizer and add ours in its place.  This is relatively easy if you've ever worked with the theme customizer.

Add the following code to your theme's `functions.php` file.

	add_action( 'customize_register', 'jt_customize_register' );

	function jt_customize_register( $wp_customize ) {

		/* Remove the WordPress background image control. */
		$wp_customize->remove_control( 'background_image' );

		/* Load our custom background image control. */
		require_once( trailingslashit( get_template_directory() ) . 'customize-control-background-image.php' );

		/* Add our custom background image control. */
		$wp_customize->add_control( new JT_Customize_Control_Background_Image( $wp_customize ) );
	}

## Registering custom backgrounds

If you studied the code from the first section above when creating the customize control class, you might have noticed the `jt_default_backgrounds` filter hook.  All you need to do to register multiple backgrounds is to add a filter on that hook and return an array of custom backgrounds.

To keep this simple and, I hope, as forward-compatible as possible, I decided to build off the method already used by the WordPress [`register_default_headers()`](http://codex.wordpress.org/Function_Reference/register_default_headers) function.

The following is an example of registering multiple default background images.  Note that you should use `%s` to reference the template (parent theme) directory and `%2$s` to reference the stylesheet (child theme) directory.

	add_filter( 'jt_default_backgrounds', 'jt_default_backgrounds' );

	function jt_default_backgrounds( $backgrounds ) {

		$backgrounds['example-1'] = array(
			'url'           => '%s/images/backgrounds/example-1.png',
			'thumbnail_url' => '%s/images/backgrounds/example-1-thumb.png',
		);

		$backgrounds['example-2'] = array(
			'url'           => '%s/images/backgrounds/example-2.png',
			'thumbnail_url' => '%s/images/backgrounds/example-2-thumb.png',
		);

		$backgrounds['example-3'] = array(
			'url'           => '%s/images/backgrounds/example-3.png',
			'thumbnail_url' => '%s/images/backgrounds/example-3-thumb.png',
		);

		return $backgrounds;
	}

A couple of things worth noting are:

* I'm using the `/images/backgrounds` directory to house my images.  So, you'll want to change that if doing something different.
* The `thumbnail_url` key is not required.  The script will fallback to the `url` key if `thumbnail_url` doesn't exist.

## Add a little extra awesomeness to your theme

Now that you can add multiple default backgrounds to your theme, you'll be able to match them up with your custom headers.  Let me know if you use this in one of your themes.  I'd love to check it out.

If you'd like to see this added to WordPress code, get involved with the [Trac ticket](http://core.trac.wordpress.org/ticket/18623).