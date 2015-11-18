# Customizer typography project

<img src="http://justintadlock.com/blog/wp-content/uploads/2015/06/customize-typography-screen.png" alt="Customizer Typography Screenshot" width="1154" height="640" class="aligncenter size-full wp-image-7225" />

Over the past few weeks, I've been giving some thought about building a typography control class for the WordPress customizer.  I started to write a tutorial on the process, but such a tutorial would probably be in the neighborhood of 4,000 words.  With something so highly technical, I didn't think a tutorial would be the best method of grasping the subject matter.

Yesterday, I had an afternoon of free time to devote to this and came up with a proof-of-concept plugin for the idea.

If you just want to skip the rest of this article, hop over to the [Customizer Typography](https://github.com/justintadlock/customizer-typography) GitHub repo and play around with it.  It's only meant for development purposes and to show one method of executing the idea.

## The approach

There were several considerations when building a typography tool for the customizer.  The most important was not having to add tons of code while still providing the developer complete control over each setting.

Generally, when adding controls for such a thing, you'd have to follow a specific process:

* Add setting for font family.
* Add control for font family.
* Add setting for font weight.
* Add control for font weight.
* Add setting for font style.
* Add control for font style.
* Add setting for font size.
* Add control for font size.
* Add setting for line height.
* Add control for line height.

I wanted to simplify that.  Fortunately, the Customization API in WordPress is pretty powerful and allows you to tie multiple settings to a single control.  This simplifies the above process to:

* Add setting for font family.
* Add setting for font weight.
* Add setting for font style.
* Add setting for font size.
* Add setting for line height.
* Add single customizer control.

That's not an insignificant amount of code that we just got rid of.  Just to give you an idea of how all of this works, take a look at the following code from the plugin.

	$wp_customize->add_setting( 'p_font_family', array( 'default' => 'Arial',  'sanitize_callback' => 'sanitize_text_field', 'transport' => 'postMessage' ) );
	$wp_customize->add_setting( 'p_font_weight', array( 'default' => '400',    'sanitize_callback' => 'absint',              'transport' => 'postMessage' ) );
	$wp_customize->add_setting( 'p_font_style',  array( 'default' => 'normal', 'sanitize_callback' => 'sanitize_key',        'transport' => 'postMessage' ) );
	$wp_customize->add_setting( 'p_font_size',   array( 'default' => '16',     'sanitize_callback' => 'absint',              'transport' => 'postMessage' ) );
	$wp_customize->add_setting( 'p_line_height', array( 'default' => '32',     'sanitize_callback' => 'absint',              'transport' => 'postMessage' ) );

	$wp_customize->add_control(
		new Customizer_Typo_Control_Typography(
			$wp_customize,
			'p_typography',
			array(
				'label'       => esc_html__( 'Paragraph Typography', 'ctypo' ),
				'description' => __( 'Select how you want your paragraphs to appear.', 'ctypo' ),
				'section'     => 'p_typography',
				'settings'    => array(
					'family'      => 'p_font_family',
					'weight'      => 'p_font_weight',
					'style'       => 'p_font_style',
					'size'        => 'p_font_size',
					'line_height' => 'p_line_height',
				),
				'l10n'        => array() // Custom labels if wanted.
			)
		)
	);

I could've simplified it further, but it would've come at the cost of decreased flexibility.  This seems to be a good balance that exposes the API to developers rather than tucking it all behind something custom.

## Feedback and patches welcome

Grab a copy of the [Customizer Typography](https://github.com/justintadlock/customizer-typography) plugin and play around with it a bit.  Let me know what you think and see if you can improve on it.