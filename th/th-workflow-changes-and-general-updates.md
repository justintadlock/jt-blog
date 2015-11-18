Unless this has changed recently, I don't think `wp_*_script()` handles conditionals.  You'll need to manually write out the `<link>` and hook it to `wp_head` or `wp_footer`.

As far as checking the page, you'd just do it like so:

`
if ( is_page( 'about' ) )
	wp_enqueue_script();
`

Reference:
http://codex.wordpress.org/Conditional_Tags