## A look into the WP_Customize_Control class

I've been working on bringing you all some great customizer tutorials such as the [multiple checkbox control](http://justintadlock.com/archives/2015/05/26/multiple-checkbox-customizer-control).  However, I'm quickly realizing that I'll need to explain certain things over and over in each tutorial.  Therefore, I wanted to cover the foundation for these tutorials in one place.  That way, I can just point people with questions to this tutorial.

The customizer is a powerful tool in the right hands.  A good portion of it is an extendable set of classes for building panels, sections, settings, and controls.  These four classes are:

* `WP_Customize_Panel`
* `WP_Customize_Section`
* `WP_Customize_Setting`
* `WP_Customize_Control`

The last class, `WP_Customize_Control`, is the class that will most often be extended by developers.  That's what I want to focus on in this tutorial.  This will mostly be a reference to point out items that are available to you to work with.

## Properties

The `WP_Customize_Control` has several properties that you can overwrite, use, or manipulate in some way in your sub-class.

### `$instance_count` property

This is a `protected` property.  It stores the number of times the class has been used to add a control in the customizer.  This is particularly useful if you need to run something based on the number of times the control is used.

	if ( 5 === $this->instance_count ) {
		// Run some code if we have 5 instances.
	}

### `$instance_number` property

This works alongside the `$instance_count` property.  It stores the current instance of the class in relation to the other instances.  This can often be useful for running something on the first load but not subsequent loads.

	if ( 1 === $this->instance_count ) {
		// Load something if first instance.
	}

### `$manager` property

This is the customizer object.  You're most likely used to seeing it as `$wp_customize`.  I've found it useful when gathering information about the customizer configuration that's not available within the control.  For example, when dealing with controls, you know the name of the setting attached to them.  However, you might want to get something about that setting.

	$setting_default = $manager->get_setting( 'setting_name' )->default;

Or, you can even add new panels, sections, settings, and/or controls from within your sub-class.

	$manager->add_panel();
	$manager->add_section();
	$manager->add_setting();
	$manager->add_control();

There are loads of possibilities.

## `$id` property

This is the control ID added via `$wp_customize->add_control( $id )`.  I've found it useful when building custom form fields and needing an ID for various reasons.

	<label for="<?php echo esc_attr( "field-{$id}" ); ?>">

## `$settings` property

Believe it or not, you can actually have multiple settings tied to an individual control.  Nearly always, there's only one setting tied to any given control.  However, for those instances where you need to use multiple, this is one way to access them.

	$setting_default = $this->settings['default'];
	$setting_data    = $this->settings['data'];

`default` is always the primary setting for a control unless changed, which brings us to:

### `$setting` property

This is the array key for the primary setting.  So, if you're passing in multiple settings as an array, the main one will have the `default` key.  However, you can change this by declaring the property in your sub-class

	public $setting = 'some-custom-key';

### `$priority` property

This is the priority for the control passed in via `$wp_customize->add_control()`.  It defaults to `10`.  I haven't found much use for it other than setting a different default like so:

	public $priority = 55;

### `$section` property

This is the ID for the section the control is being used in.  You could use it along with the `$manager` property to get data about the section.

	$section_title = $manager->get_section( $this->section )->title;

### `$label` property

This is the label used for the control.  You'll most likely be using it in the `render_content()` method (see methods section of this tutorial) to print the label to the screen

	<?php if ( !empty( $this->label ) ) : ?>
		<span class="customize-control-title"><?php echo esc_html( $this->label ); ?></span>
	<?php endif; ?>

### `$description` property

Like the `$label` property, you'll use it to print the description to the screen.

	<?php if ( !empty( $this->description ) ) : ?>
		<span class="description customize-control-description"><?php echo $this->description; ?></span>
	<?php endif; ?>


	public $choices = array();

	/**
	 * @access public
	 * @var array
	 */
	public $input_attrs = array();

	/**
	 * @access public
	 * @var string
	 */
	public $type = 'text';

	/**
	 * Callback.
	 *
	 * @since 4.0.0
	 * @access public
	 *
	 * @see WP_Customize_Control::active()
	 *
	 * @var callable Callback is called with one argument, the instance of
	 *               WP_Customize_Control, and returns bool to indicate whether
	 *               the control is active (such as it relates to the URL
	 *               currently being previewed).
	 */
	public $active_callback = '';