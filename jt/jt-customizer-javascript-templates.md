In my previous tutorial on building a [radio image control](http://justintadlock.com/archives/2015/06/04/customizer-radio-image-control) in the WordPress customizer, instead of using PHP to output data for the control output, I used JS.  Specifically, this used [Underscore's](http://underscorejs.org/) templating engine that's packaged with WordPress.

While I'm not well-versed in JavaScript, it's something that will increasingly become standard for customizer controls and, most likely, other parts of WordPress in the future. Therefore, it's something that all serious WP developers need to be studying and using.

Unfortunately, understandable documentation and tutorials are few and far between, which is bit crazy considering we've had Underscore.js in core since version 3.5. It might take a bit of trial-and-error and reading core code examples to figure things out.

When using a JS templating engine, you remove the PHP logic and just have a single template that's reused.  What changes is the data that gets output.  This could also be done on the fly.  It's pretty powerful stuff when you think of some of the possibilities.

In this tutorial, I'm going to cover some of the things I've learned so far while working with JS templates in the customizer.  If you want to check out some real-world code examples, I highly encourage looking over the [customize folder](https://github.com/justintadlock/hybrid-core/tree/dev/customize) in the upcoming version of Hybrid Core.

## Mustache-inspired syntax

Because Underscore's syntax will cause a fatal error on any WordPress site with `asp_tags` enabled in their `php.ini` file, core couldn't use that.  So, WP uses [{{ mustache }}](https://mustache.github.io/)-inspired template tags.

There are three tags you need to know:

* `<# #>` - Used for executing JavaScript code.
* `{{ }}` - Used for outputting escaped data.
* `{{{ }}}` - Used for outputting unescaped data such as HTML.

Once you get the hang of how those work, it's pretty easy to make the jump from the PHP-coded output that you might be used to.

## Building custom controls

I won't cover the ins-and-outs of creating custom control classes.  That's outside the scope of this tutorial.  Otto has a great tutorial on [building controls](http://ottopress.com/2012/making-a-custom-control-for-the-theme-customizer/) that you can follow.  Think of this as the next step.

### Registering your control

I'm going to assume you have a custom control named `JT_Customize_Control_Select` in a file named `/customize/control-select.php` in your theme for the purposes of this tutorial.  It's going to output a basic `<select>`.  Yes, core has a select option built in, but we just need a basic example.

In order to register your control type, you need to utilize the `WP_Customize_Manager::register_control_type()` method.  This is important because we need WP to recognize our JS template output.

Here's an example of how that'd look in your theme:

	add_action( 'customize_register', 'jt_customize_register' );

	function jt_customize_register( $wp_customize ) {

		// Load our custom control.
		require_once( trailingslashit( get_template_directory() ) . 'customize/control-select.php' );

		// Register the control type.
		$wp_customize->register_control_type( 'JT_Customize_Control_Select' );
	}

As you can see, we just used the class name to register it.

### Sending PHP data to JavaScript

If using JavaScript to build templates, we need a method for getting the data.  That's where the `WP_Customize_Control::to_json()` method comes in.  In your custom control class, you'll need to create that method to send over any data you'd like to use.

Let's take a look at what a custom `to_json()` method might look like for a custom select control:

	public function to_json() {

		// Call parent to_json() method to get the core defaults like "label", "description", etc.
		parent::to_json()

		// The setting value.
		$this->json['value'] = $this->value();

		// The control choices.
		$this->json['choices'] = $this->choices;

		// The data link.
		$this->json['link'] = $this->get_link();
	}

## Building the JS template

For those of you familiar with creating custom controls with PHP, you're probably used to overwriting the `WP_Customize_Control::render_content()` method.  Instead, we'll overwrite the `content_template()` method for JS templating.

So, if you were building a `<select>` output, it would look something like the following.  This is where we'll be using the data passed from the `to_json()` method in the previous step.

	public function content_template() { ?>

		<# if ( ! data.choices ) {
			return;
		} #>

		<label>

			<# if ( data.label ) { #>
				<span class="customize-control-title">{{ data.label }}</span>
			<# } #>
	
			<# if ( data.description ) { #>
				<span class="description customize-control-description">{{{ data.description }}}</span>
			<# } #>
	
			<select {{{ data.link }}}>
	
				<# for ( key in data.choices ) { #>
	
					<option value="{{ key }}" <# if ( key === data.value ) { #> checked="checked" <# } #>>{{ data.choices[ key ] }}</option>
	
				<# } #>
	
			</select>

		</label>
	<?php }

As you can see, the method utilizes the Mustache syntax to output the data.  It's not a huge stretch if you're used to working with PHP.  Keep note of where double braces, `{{`, and triple braces, `{{{` are used.  You want to make sure your data is escaped when it needs to be escaped.

### Setting the data

One thing you might have noticed if you've built something with the code above is that the "Save and Publish" button is not triggered nor is the data saved.  We'll need to do that with JS too.

I always create a custom JS file called `customize-controls.js` and put it in my theme's `/js` folder.  There are two things you'll need in your control class for this.  The first is you need to define the `$type` property to something custom (should be doing this anyway).

	public $type = 'jt-select`;

The next is you need to create the `enqueue()` method to load your script:

	public function enqueue() {
		wp_enqueue_script( 'jt-customize-controls', get_template_directory_uri() . '/js/customize-controls.js', array( 'jquery' ) );
	}

Then, you need to use the following in the in your script file:

	wp.customize.controlConstructor['jt-select'] = wp.customize.Control.extend( {
		ready: function() {
			var control = this;
	
			this.container.on( 'change', 'select',
				function() {
					control.setting.set( jQuery( this ).val() );
				}
			);
		}
	} );

There may be a much better way of handling that.  Feedback is more than welcome.

## Comments? Feedback?

As I said, this is entirely new territory for me.  The best way I can learn how to do this is to put it into practical application and to write about it.

If you have any corrections or better methods for doing this, don't hesitate to let me know in the comments.  Otherwise, I hope you've found this tutorial helpful.