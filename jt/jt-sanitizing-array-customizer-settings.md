## Sanitizing array customizer settings

In my previous tutorial on building a [multiple checkbox customizer control](http://justintadlock.com/archives/2015/05/26/multiple-checkbox-customizer-control), I needed a way of sanitizing an array of values for a single setting.  That's generally pretty simple as far as PHP goes.  Just create a callback function and use your sanitize callback within `array_map()`.

I got to thinking about a better way of doing that so that I didn't need to continue writing custom functions each time I had an array setting.  So, I came up with a custom setting class.

## Building the setting class

To use the setting class, copy the following code to the `/customize` folder in your theme in a file called `setting-array-map.php` (or whatever you prefer for your theme structure).

	/**
	 * Handles an array of values by running the `sanitize_callback` through `array_map()`.
	 *
	 * @since  1.0.0
	 * @access public
	 */
	class JT_Customize_Setting_Array_Map extends WP_Customize_Setting {
	
		/**
		 * The sanitize callback function to run over each element of the array.
		 *
		 * @since  1.0.0
		 * @access public
		 * @var    string
		 */
		public $sanitize_callback = 'sanitize_text_field';
	
		/**
		 * Sanitize the array values.  This method overwrites the parent `sanitize()` method and 
		 * runs `array_map()` over the multiple values.  Expected input is an array of values or 
		 * a comma-separated list of values.
		 *
		 * @since  1.0.0
		 * @access public
		 * @param  array|string  $values
		 * @return array
		 */
		public function sanitize( $values ) {
	
			$multi_values = !is_array( $values ) ? explode( ',', $values ) : $values;
	
			return !empty( $multi_values ) ? array_map( array( $this, 'map' ), $multi_values ) : array();
		}
	
		/**
		 * Callback function for `array_map()`.  Uses the defined `sanitize_callback` to filter 
		 * each element of the array.
		 *
		 * @since  1.0.0
		 * @access public
		 * @param  mixed  $value
		 * @return mixed
		 */
		public function map( $value ) {
	
			return apply_filters( "customize_sanitize_{$this->id}", $value, $this );
		}
	}

## Using the setting class

I'll just copy/paste the setting code from the previous tutorial to keep things simple.  Here's how you'd use the custom setting class.

	add_action( 'customize_register', 'jt_customize_register' );

	function jt_customize_register( $wp_customize ) {

		require_once( trailingslashit( get_template_directory() ) . 'customize/setting-array-map.php' );

		$wp_customize->add_setting(
			new JT_Customize_Setting_Array_Map(
				$wp_customize,
				'favorite_fruit',
				array(
					'default'           => array( 'apple', 'orange' ),
					'sanitize_callback' => 'sanitize_key'
				)
			)
		);
	}

What will happen is our custom `sanitize_callback` will be run over each item of the array.  In this particular case, I'm using `sanitize_key`, but you can use anything you want.