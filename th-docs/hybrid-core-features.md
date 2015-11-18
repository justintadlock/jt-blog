Hybrid Core features are modular PHP scripts that you may optionally add to your theme.  Some themes may require many or all of the features while other projects may only use a few.  It's entirely up to you as the theme developer.

In the [theme setup tutorial](http://themehybrid.com/docs/hybrid-core-setup), you learned how to register support for framework features in your theme setup function.  Below is a list of the available features and a quick snippet of code you can copy and paste into your theme setup function for each.

## [Template Hierarchy](http://themehybrid.com/docs/template-hierarchy)

Overwrites the default WordPress theme template hierarchy with a much more flexible and powerful templating system.

	add_theme_support( 'hybrid-core-template-hierarchy' );

## [Theme Layouts](http://themehybrid.com/docs/theme-layouts)

Adds custom theme layouts.

	add_theme_support( 'theme-layouts', array( 'default' => '2c-r' ) );

## Deprecated

Loads all the deprecated functions in case you need to account for backwards compatibility.

	add_theme_support( 'hybrid-core-deprecated' );