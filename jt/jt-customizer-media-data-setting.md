## Customizer: How to save image (media) data

A couple of weeks ago, the WordPress.org Theme Review Team (TRT) announced that we'd be requiring theme options to go through the customizer rather than custom settings screens.  I wrote the post [explaining the details](https://make.wordpress.org/themes/2015/04/22/details-on-the-new-theme-settings-customizer-guideline/) of our settings guideline change.  

In that post, I volunteered my coding services for building custom controls for anyone who asked.  Unfortunately, not many took me up on that offer.  However, [Kadence Themes](http://kadencethemes.com/) stepped up with a few requests.

<img src="http://justintadlock.com/blog/wp-content/uploads/2015/05/example-customizer-image.png" alt="Example Customizer Image Control" width="300" height="414" class="alignright size-full wp-image-7141" />

Specifically, one item they asked for was a "media field that holds an array so width, height and attachment id are stored."

Technically, that's not a customizer control.  That deals with customizer settings.  However, I thought it was an awesome idea because WordPress would normally only store the media URL.  There are times when you need more information.

In this tutorial, I'm just focusing on saving image data, but you can extend it to work with other media types as well.

## Prerequisites

At this point, I'll assume you're a theme developer who has worked with the [Customizer API](http://developer.wordpress.org/themes/advanced-topics/customizer-api/) and understand how controls and settings work.

You need to know where and how to integrate customizer code into your theme.  That's a whole other tutorial that's been covered <em>ad nauseum</em> around the Web.  This is a high-level theme customizer tutorial, so I'm mostly just sharing code rather than explaining the details.

## Creating a custom setting class

There's very little that has been written on extending the `WP_Customize_Setting` class.  This is actually my first time doing it, so it's possible I get things wrong.  You can learn from my mistakes if I do.

Here's the class we'll need for saving image data:

	<?php
	/**
	 * Custom class for saving media data in an array. Only supports the 'theme_mod' type.
	 *
	 * @author     Justin Tadlock <justin@justintadlock.com>
	 * @copyright  Copyright (c) 2015, Justin Tadlock
	 * @link       http://themehybrid.com/hybrid-core
	 * @license    http://www.gnu.org/licenses/old-licenses/gpl-2.0.html
	 */
	class JT_Customize_Setting_Image_Data extends WP_Customize_Setting {
	
		/**
		 * Overwrites the `update()` method so we can save some extra data.
		 */
		protected function update( $value ) {
	
			if ( $value ) {
	
				$post_id = attachment_url_to_postid( $value );
	
				if ( $post_id ) {
	
					$image = wp_get_attachment_image_src( $post_id );
	
					if ( $image ) {
	
						/* Set up a custom array of data to save. */
						$data = array(
							'url'    => esc_url_raw( $image[0] ),
							'width'  => absint( $image[1] ),
							'height' => absint( $image[2] ),
							'id'     => absint( $post_id )
						);
	
						set_theme_mod( "{$this->id_data[ 'base' ]}_data", $data );
					}
				}
			}
	
			/* No media? Remove the data mod. */
			if ( empty( $value ) || empty( $post_id ) || empty( $image ) )
				remove_theme_mod( "{$this->id_data[ 'base' ]}_data" );
	
			/* Let's send this back up and let the parent class do its thing. */
			return parent::update( $value );
		}
	}

This is very basic and only makes use of the `theme_mod` type of setting.  You can build upon that if you wish.

## Adding the setting and control

This step works like setting up any other customizer settings and controls.  For this, I'm just sticking a core WP image control in the `title_tagline` section and tying it to our setting.

The important bit is adding the setting.  Note how I reference `JT_Customize_Setting_Image_Data` so that we can utilize our custom setting class.

	<?php

	add_action( 'customize_register', 'jt_customize_register' );

	function jt_customize_register( $wp_customize ) {

		$wp_customize->add_setting(
			new JT_Customize_Setting_Image_Data(
				$wp_customize,
				'example_image',
				array( 'default' => get_theme_mod( 'example_image', '' ) )
			)
		);

		$wp_customize->add_control(
			new WP_Customize_Image_Control(
				$wp_customize,
				'example-image-control',
				array(
					'label'       => esc_html__( 'Example Image', 'example-textdomain' ),
					'section'     => 'title_tagline',
					'settings'    => 'example_image'
				)
			)
		);
	}

## Getting the theme settings

OK, so we've got the customizer part set up, but we still need to be able to get the data.  You'll notice that I added the `example_image` setting above.  That will have the image URL.  However, you can also access the data via the `example_image_data` setting.

Here's some examples:

	// String: Image URL
	$url = get_theme_mod( 'example_image' );

	// array( 'url' => $url, 'width' => $width, 'height' => $height, 'id' => $attachment_id )
	$data = get_theme_mod( 'example_image_data' );

## Conclusion

After studying how this was handled in core (check header image customizer stuff), I noticed that there are many methods to actually doing this.  I was mostly looking for an easy, reusable route to getting image/media data. I also thought it'd be a good time to experiment with a custom setting class. I'd certainly be happy to look at alternative solutions. 

For example, you could certainly hook into `customize_save_{$setting_id}` and handle this on a per-setting basis.

Also, my offer of helping out with customizer controls still stands for folks who want to take me up on that.