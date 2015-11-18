The purpose of the `Hybrid` class is to encapsulate the initialization and setup process of the Hybrid Core framework.  This is meant to be called only once to get things going.

## Usage

To build a theme off the Hybrid Core framework, you must call this class in your theme's `functions.php` file, preferably before any other code.  Use the following code block to initialize the framework.

	require_once( trailingslashit( get_template_directory() ) . 'hybrid-core/hybrid.php' );

	new Hybrid();

## Methods

The following is a list of the class methods for reference.

* `__construct()`: Constructor method, which launches the framework.
* `constants()`: Defines the constant paths for use within the core framework, parent theme, and child theme. 
* `core()`: Loads the core framework functions.  These files are needed before loading anything else in the framework because they have required functions for use.
* `theme_support()`: Adds theme support for specific features.  Removes theme supported features from themes in the case that a user has a plugin installed that handles the functionality.
* `includes()`: Loads the framework functions.  Many of these functions are needed to properly run the framework.  Some components are only loaded if the theme supports them.
* `extensions()`: Load extensions (external projects).  Extensions are projects that are included within the framework but are not a part of it.  They are external projects developed outside of the framework.
* `admin()`: Load admin files for the framework.

## Extending the class

Currently, the class isn't very useful for creating other classes to extend it.  The class is meant to be a singleton and only used once.