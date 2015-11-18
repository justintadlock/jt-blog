Once you've downloaded the Hybrid Core package, you'll want to install it into your theme.  I'm going to assume from this point forward that you're creating a WordPress theme from scratch.  You can certainly integrate the framework into a preexisting theme, but this is not the recommended method.

Understanding what's presented in this guide will pretty much teach you everything you need to know about *using* the framework.  There are other topics that go into more detail and show you neat things you can do, but this is the backbone of how Hybrid Core works.  It's essential that you follow the conventions laid out here.

You should also already be familiar with WordPress [theme development](http://codex.wordpress.org/Theme_Development) at this point.  This is not a guide for creating WordPress themes.  It's a guide on teaching theme developers how to use the framework.

## Adding the framework to a theme

Let's assume you're creating a WordPress theme called "Super Mario".  You should have already created a folder for this theme called `super-mario` and added a `style.css` file with your theme information in it.

Within your `super-mario` folder, you need to add the framework folder.  When you downloaded it, you should've gotten a folder (after unzipping it) called `hybrid-core` with other folders and files within it.  Add this `hybrid-core` folder into your theme.

<p class="alert">You can technically change the `hybrid-core` folder name to anything you like or leave it the same.  Personally, I like calling it `library`.  Just be sure any references you make to it are correct.</p>

## Loading the framework

Now that you've added the framework to your theme, you'll want to load it.

If you haven't already done so, create a file called `functions.php` within your theme.  Add the below code to this file (this should be the only code in the file at this point).

	<?php

	// Set up the Hybrid Core framework.
	require_once( trailingslashit( get_template_directory() ) . 'hybrid-core/hybrid.php' );
	new Hybrid();
	
	// Theme PHP code below this line.

That's all you have to do to load and initialize the framework.

## Theme setup

Just because you've loaded the framework, doesn't mean you're really using much of it.  Nearly all of Hybrid Core's features are turned off by default or have to be integrated directly in your theme.  The reason for this is that it allows you to only work with the features that you want to use.  It's an extremely modular system, so you can mix-and-match all kinds of things.  

Before you can dive into using the framework, you need to create a theme setup function.

I actually recommend *always* creating a theme setup function, even if you're not creating a theme based on the framework.  It's good practice because it keeps your code organized and allows others to know exactly when certain code is executing.

Note this line in your `functions.php` file that you added:

	// Theme PHP code below this line.

Below this, you can build your theme setup function.  While this is certainly not a requirement and there are many ways to handle this, I've found the method I'll describe here the best.  The phrase "theme setup function" will be used throughout the documentation and in the support forums.  It's important that you understand what this is.

You'll want to add your theme setup function to the `after_setup_theme` action hook with a priority of `10` (the default) or earlier.  I like to set my themes up with a priority of `5` so that it's easier for child theme developers to hook in at the default.  It's important that you don't add this function with a higher priority though.  The framework loads things at specific points, so trust that this is the best way to handle this.

	add_action( 'after_setup_theme', 'super_mario_theme_setup', 5 );

	function super_mario_theme_setup() {
		
		// add_theme_support() calls go here.
	
		// add_action() and add_filter() calls go here.	
	}

<p class="alert">Notice that I prefixed the function name with `super_mario_`?  It is good development practice to prefix your function names consistently, typically using the theme name as the prefix.</p>

## Adding framework features and extensions

As mentioned earlier, Hybrid Core is a modular system.  This means that you get to choose what features you want to use from it.  Fortunately, WordPress has a system in place for handling this.  You'll be using the [add_theme_support()](http://codex.wordpress.org/Function_Reference/add_theme_support) function to "register" support for certain features of the framework.

Let's take a look at how this function would look when registering support for the framework's custom template hierarchy:

	add_theme_support( 'hybrid-core-template-hierarchy' );

Simple, right?  One line of code and you've added a new feature.  This is probably one of the most innovative theme-related features of WordPress.  What the above line of code would do is tell Hybrid Core that the theme wants to use its built-in template hierarchy over WordPress'.

Going back to your theme setup function from above, you have this line:

	// add_theme_support() calls go here.

Any time you want to register support of a new feature, you simply add a new line below that.

There are various features that you can add support for.  This is kind of the *magic* of the framework. Hybrid Core technically has two types of features you can register support for:  [features](http://themehybrid.com/docs/hybrid-core-features) and [extensions](http://themehybrid.com/docs/hybrid-core-extensions)

## Adding filters and actions

Learning how to add action and filters to hooks is well outside the scope of this guide.  You'll need to consult the WordPress [documentation](http://codex.wordpress.org/Plugin_API) for more details on this.

The reason this section exists is to point out where your calls to `add_action()` and `add_filter()` should go.  Many themes get things wrong and have stuff randomly placed in their `functions.php` files.  You've got a theme setup function.  Use it and keep things organized.

In your theme setup function, you added this line:

	// add_action() and add_filter() calls go here.	

You would add any action and filter calls after this.  For example, if you wanted to filter the `sidebars_widgets` with a custom function called `super_mario_sidebars_widgets`, you'd add it directly below that line:

	add_filter( 'sidebars_widgets', 'super_mario_sidebars_widgets' );

## Putting it all together

This entire tutorial has been about keeping your code organized so that you can make the best WordPress theme possible.  You've learned how to put this thing together.  Now, I'll let you look at a more advanced example of a `functions.php` file and see how it all comes together.

	<?php

	// Set up the Hybrid Core framework.
	require_once( trailingslashit( get_template_directory() ) . 'hybrid-core/hybrid.php' );
	new Hybrid();

	# Theme setup
	add_action( 'after_setup_theme', 'super_mario_theme_setup', 5 );

	/**
	 * Sets up the Super Mario theme.
	 *
	 * @since  1.0.0
	 * @access public
	 * @return void
	 */
	function super_mario_theme_setup() {
		
		// Add support for the template hierarchy.
		add_theme_support( 'hybrid-core-widgets' );
	
		// Add theme support for WordPress features.
		add_theme_support( 'automatic-feed-links' );
		add_custom_background();

		// Register sidebars.
		add_action( 'widgets_init', 'super_mario_register_sidebars', 11 );
	
		// Filter the sidebar widgets.
		add_filter( 'sidebars_widgets', 'super_mario_disable_sidebars' );
	}

	/**
	 * Fictional function to register sidebars.
	 */
	function super_mario_register_sidebars() {
		return false;
	}
	
	/**
	 * Fictional function to disable sidebars.
	 */
	function super_mario_disable_sidebars( $sidebars_widgets ) {
		return $sidebars_widgets;
	}

That should give you something to go on.  If you're wanting to look at a real-world example of the framework in use of a theme, all themes at Theme Hybrid are built on the Hybrid Core framework.