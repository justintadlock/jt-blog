# Adding title tag support

As of today's team meeting, <code>title-tag</code> support is now required for all themes.  We keep a back-compatibility policy of two versions, and the title tag feature was added in WordPress 4.1.  So, we're at that point.

The team has put up a <a href="https://github.com/Otto42/theme-check/issues/84">ticket</a> to get this added to the Theme Check plugin, so it should be an automatic check with no need for manual checking from reviewers once it gets rolled in.

This post is primarily a heads up for theme authors.

<h2>Do I have to change my code?</h2>

It depends.  I think most new themes are already adding support.  If not, you simply need to add a single line within your theme setup function, which would look something like the following.

<pre><code>add_action( 'after_setup_theme', 'theme_slug_setup' );

function theme_slug_setup() {

	add_theme_support( 'title-tag' );
}</code></pre>

<h2>Removing back-compat code</h2>

If you previously had code to handle pre-4.1 installs, you can simply remove it.  That code would look something like this:

<pre><code>if ( ! function_exists( '_wp_render_title_tag' ) ) {
	function theme_slug_render_title() {
?>
&lt;title>&lt;?php wp_title( '|', true, 'right' ); ?>&lt;/title>
&lt;?php
	}
	add_action( 'wp_head', 'theme_slug_render_title' );
}</code></pre>

Also, make sure the following is not in your <code>header.php</code> template:

<pre><code>&lt;title>&lt;?php wp_title( '|', true, 'right' ); ?>&lt;/title></code></pre>