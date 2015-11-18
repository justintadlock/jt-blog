# Backward-compatible favicons/icons

As of WordPress 4.3, core includes a new site icon feature, which covers favicons and a few other icons.  Now that it's in core, it's time to start phasing this feature out of themes.

One of our guidelines is that themes should use core functionality where possible.  Because this is now core functionality, new themes shouldn't be adding this feature in.

<h2>Providing back compatibility</h2>

If you already have a theme that supports favicons, you'll want to update your code in a way that doesn't make users' old favicons suddenly disappear, making for a smooth transition.

The easiest method of doing this is first checking if the <code>has_site_icon()</code> function exists.  This will let you know that the user is on WP 4.3 and has the site icon feature available.

To make it even smoother, you can also check that the user has set up a new icon using the core WP feature.  <code>has_site_icon()</code> is a conditional tag and will return <code>TRUE</code> or <code>FALSE</code>.

Here's a bit of example code to handle the check:

<pre><code>if ( ! function_exists( 'has_site_icon' ) || ! has_site_icon() ) {

    // Output old, custom favicon feature.
}</code></pre>

Then, when WP 4.5 or so rolls around, you'll be able remove the feature completely.