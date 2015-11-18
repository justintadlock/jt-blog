Theme Layouts is a Hybrid Core feature that allows theme developers to create multiple, selectable layouts for users of their themes.

Currently, users can select a layout via the customizer or on a per-post basis via a meta box on the edit post screen labeled "Layout."

## Adding theme support for Theme Layouts

To enable the Theme Layouts extension, add the following line of code to your theme setup function.

	add_theme_support( 'theme-layouts', array( 'default' => '2c-l' ) );

This code merely registers support for the script.  It doesn't do anything else. The second parameter of the `add_theme_support()` call supports the following arguments:

* `default` - The name of the default layout (see registering layouts below).
* `customize` - Whether to show the layout selector in the customizer.  Default `true`.
* `post_meta` - Whether to show the layout post meta box.  Default `true`.

## Registering layouts

Even though you've added support for the feature, you need to register some layouts.  For this, you need to hook into `hybrid_register_layouts` and register each layout with the `hybrid_register_layout()` function like so:

	add_action( 'hybrid_register_layouts', 'my_register_layouts' );

	function my_register_layouts() {

		hybrid_register_layout( '2c-l', array( 'label' => esc_html__( 'Content / Sidebar', 'my-textdomain' ), 'image' => '%s/images/layout-2c-l.png' ) );

		hybrid_register_layout( '2c-r', array( 'label' => esc_html__( 'Sidebar / Content', 'my-textdomain' ), 'image' => '%s/images/layout-2c-r.png' ) );
	}

The `hybrid_register_layout()` function accepts two parameters:

	hybrid_register_layout( $name, $args );

The `$name` parameter is the name of the layout.  It should only contain alphanumeric characters, hyphens, and/or underscores.

The `$args` parameter is an array of available arguments.  Here are the defaults:

		$defaults = array(
			'is_global_layout' => true,    // Whether to show as an option in the customizer.
			'is_post_layout'   => true,    // Whether to show as an option in the meta box.
			'is_user_layout'   => true,    // Whether to show as an option in user profile (not implemented).
			'label'            => $name,   // Internationalized text label.
			'image'            => '',      // Image URL of the layout design.
			'post_types'       => array(), // Array of post types layout works with.
		);

Note that you should always include an `image` URL.  Otherwise, the layout will not appear.

## Styling your layouts

I can't tell you what CSS to write for your theme.  You're building something custom, so it'd look completely different from what I'd do for my theme.

Layouts are added to the `<body>` class in the form of `layout-xxx`.  So, if the user selected the `2c-r` layout you registered earlier, the layout class would be `layout-2c-r`.

With the default layout options (if using them all), you have the following layout classes.

## Available functions

There are several functions available in the Layouts API.  For the purposes of this tutorial and general theme usage, the most important functions are shown in this section.

### hybrid_register_layout()

Registers a layout (see notes above).

	hybrid_register_layout( $name, $args );

### hybrid_unregister_layout()

Used to unregister an existing layout by name.

	hybrid_unregister_layout( $name );

### hybrid_layout_exists()

Conditional tag used to check if a layout already exists.

	hybrid_layout_exists( $name );

### hybrid_get_layouts()

Returns an array of registered layout objects.

	hybrid_get_layouts();

### hybrid_get_layout()

Returns a single layout object.

	hybrid_get_layout( $name );

### hybrid_get_theme_layout()

Returns the name of the current layout.

	hybrid_get_theme_layout();

### hybrid_get_global_layout()

Returns the name of the layout selected via the customizer.

	hybrid_get_global_layout();

### hybrid_get_default_layout()

Returns the name of the layout defined in the `add_theme_support()` call (see above).

	hybrid_get_default_layout();

### hybrid_get_post_layout()

Returns the layout for a specific post.

	hybrid_get_post_layout( $post_id );

### hybrid_has_post_layout()

Conditional tag to check if the current post has a layout.

	hybrid_has_post_layout( $layout, $post_id = '' );

### hybrid_get_user_layout()

Returns the layout for a specific user.

	hybrid_get_user_layout( $user_id );

### hybrid_has_user_layout()

Conditional tag to check if the current user has a layout.

	hybrid_has_user_layout( $layout, $user_id = '' );