# Using theme mod defaults

As more and more theme authors begin to make the move to the customizer, many are also making the switch to storing theme options as theme mods rather than rolling a custom database option.  This is awesome because theme mods have a bit more to offer.

One of the common mistakes I'm seeing is not making use of the <code>$default</code> parameter of <a href="https://developer.wordpress.org/reference/functions/get_theme_mod/">get_theme_mod()</a>:

<pre><code>get_theme_mod( $name, $default )</code></pre>

That second parameter is pretty important as you'll see below.

<h2>Common usage</h2>

The following is some common code I see in themes.

<pre><code>$example = get_theme_mod( 'example' );

if ( $example ) {

	echo $example;

} else {

	echo 'Some default';
}</code></pre>

While that's not technically broken, it's kind of clunky and can be handled so much more elegantly as shown in this next bit of code.

<pre><code>echo get_theme_mod( 'example', 'Some default' );</code></pre>

Yep, we just cut that down to a single line.  No need for an if/else check or anything like that.  You can let WP handle the logic behind the scenes.

Basically, that tells WP to output the <code>example</code> mod.  If that mod hasn't been saved yet, output our pre-defined default.