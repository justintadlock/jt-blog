# Intro to Underscore.js templates in WordPress

The [Underscore.js library](http://underscorejs.org) has been in WordPress for many versions now. However, it's next to impossible to find good tutorials that walk you through the process of utilizing it, step-by-step.

I got my first taste of it when building templates for the WordPress customizer, but that's just outputting data in a template.  That's the easy part and not much different from HTML + PHP. I had no idea how to send the data to the template.  It was tough to find information on how to get from Point A to Point B.

I don't have a strong JavaScript background, so I felt completely lost trying to grok some of these concepts.  But, getting the basics down isn't all that hard once you have that "light-bulb moment" or have someone explain it to you like an actual beginner.  

It took me about two days to start getting comfortable working with Underscore.

In this tutorial, I want to share some basics to getting things set up and running if you want to build custom Underscore templates.  If nothing else, maybe it'll help someone that's stuck in the early learning stages of utilizing Underscore templates.

## Setting up the example

For the purposes of the tutorial, I'm just going to make the assumption that you're doing this in a theme.  So, create a basic `index.php` file and put the following code in it.

	<?php get_header(); ?>

		<div class="site-content"></div>

	<?php get_footer(); ?>

The rest of the code in the tutorial will assume you're working from your theme's `functions.php`.

## Loading Underscore.js

You'll want to enqueue the `wp-util` script to load Underscore. It changes up some of the defaults for working with the library, which allows us to use the much cooler mustache-flavored `{{` and `}}`  syntax instead of `<%` and `%>`.

You enqueue it like any other script:

	add_action( 'wp_enqueue_scripts', 'jt_enqueue_scripts' );

	function jt_enqueue_scripts() {
		wp_enqueue_script( 'wp-util' );
	}

## What are Underscore or JavaScript templates?

Templates are some HTML and "tags" mixed in.  Underscore also allows you to use any JavaScript if you need to do some logic as well.  However, the idea is to remove logic from templates as much as possible.

These templates are also reusable.  They get printed once to the page, but you can use them as often as you need.  It makes doing stuff *on the fly* pretty nice.

Here's a basic look at a template:

	<article class="post">

		<header class="entry-header">
			<h1 class="entry-title">{{ data.post_title }}</h1>
			<span class="entry-author">{{ data.post_author }}</span>
		</header>

		<div class="entry-content">
			{{{ data.post_content }}}
		</div>

	</article>

Yep, if you're paying attention, that's a basic post output.  We're replacing PHP tags with some weird-looking stuff wrapped in `{{` and `}}`.

There are three tags you'll want to know:

* `{{ var }}` is used for HTML-escaped data.
* `{{{ var }}}` is used for raw data (not escaped).
* `<# some_code() #>` allows you to evaluate any JavaScript code.

This is all pretty basic stuff.

One important thing to note is that `data` is the name of the object that will hold all the data passed to the template.  We'll cover that later.  It's just a note that your `post_title` will be `data.post_title` in the template, for example.

## Wrapping your templates

We don't want browsers just outputting our templates.  We need to let them be rendered via JS.  So, we wrap the template in `<script>` tags.  This will keep them from being rendered until it's done so via JS.

	<script type="text/html" id="tmpl-jt-post">

		<!-- Your template from the above section goes here. -->

	</script>

The important thing to note here is the `tmpl-` prefix for the `id` attribute.  Your template needs a unique ID and to have that prefix.

You'll most likely want to simply hook into `wp_footer` and output the template (wrapped in `<script>` tags) there.

	add_action( 'wp_footer', 'jt_print_post_template', 25 );

	function jt_print_post_template() { ?>

		<script type="text/html" id="tmpl-jt-post">

			<article class="post">

				<header class="entry-header">
					<h1 class="entry-title">{{ data.post_title }}</h1>
					<span class="entry-author">{{ data.post_author }}</span>
				</header>

				<div class="entry-content">
					{{{ data.post_content }}}
				</div>

			</article>

		</script>
	<?php }

## Getting PHP data into the template

Often, we'll need to pass some data from PHP to JavaScript.  For that, we'll need the `wp_json_encode()` function.  JSON (JavaScript Object Notation) is essentially a universal data-exchange format.  

For our purposes, it will create an object that we can use in JavaScript.  Since we're building templates in JavaScript, we'll need data in a format that we can use.

In the above example, we have 3 pieces of data:  post title, post author, and post content.  Let's just create a PHP array of this data to use an example:

	$json = array(
		'post_title'   => 'This is awesome!',
		'post_author'  => 'Justin Tadlock',
		'post_content' => '<p>This is the content of an example post.</p>'
	);

Of course, in a real-world project, you'd be pulling that data from a database.  For now, let's stick to the basics.

Remember that template ID from the previous section?  We're going to need that.  This is how you set up an Underscore template and pass your data in:

	<script type="text/javascript">
		jQuery( document ).ready( function() {

			var post_template = wp.template( 'jt-post' );
	
			jQuery( '.site-content' ).append( post_template( <?php echo wp_json_encode( $json ); ?> ) );
		} );
	</script>

There's a couple of things worth noting there.

* The `post_template` variable is going to be our template.
* You can pass data (a JS object) into this, which gets sent to our template from earlier.
* The `wp_json_encode()` function is used to convert the PHP data.
* I'm using a single line of jQuery to append the template output to `<div class="site-content">`.

Here's what this should look like wrapped all up:

	add_action( 'wp_footer', 'jt_print_scripts', 25 );

	function jt_print_scripts() {

		$json = array(
			'post_title'   => 'This is awesome!',
			'post_author'  => 'Justin Tadlock',
			'post_content' => '<p>This is the content of an example post.</p>'
		); ?>

		<script type="text/javascript">
			jQuery( document ).ready( function() {

				var post_template = wp.template( 'jt-post' );
	
				jQuery( '.site-content' ).append( post_template( <?php echo wp_json_encode( $json ); ?> ) );
			} );
		</script>
	<?php }

That, coupled with the earlier code, will output our post on the screen.

## Getting JS data into the template

You can also pass a JavaScript object directly into the template if you're working with data in JS rather than PHP.

Here's a look at the previous section done via JS instead:

	add_action( 'wp_footer', 'jt_print_scripts', 25 );

	function jt_print_scripts() { ?>

		<script type="text/javascript">
			jQuery( document ).ready( function() {

				var post_template = wp.template( 'jt-post' );

				var data = {
					post_title   : 'This is awesome!',
					post_author  : 'Justin Tadlock',
					post_content : '<p>This is the content of an example post.</p>'
				}

				jQuery( '.site-content' ).append( post_template( data ) );
			} );
		</script>
	<?php }

## More advanced stuff

I intentionally kept this tutorial down to the very basics.  This is my "Hello World" tutorial for using the Underscore.js library packaged with WordPress.  

If you want to see a real-world example, feel free to dig into the [Members plugin](http://themehybrid.com/plugins/members).  Underscore is used to power part of the edit capabilities and custom capability sections on the edit/new role screen.

Also, templating is but one aspect of Underscore.  It has a slew of other useful functions that are worth checking out.