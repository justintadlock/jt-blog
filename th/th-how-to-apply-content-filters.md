# How to apply "content" filters

Quite often, I see WordPress plugin developers have a bit of code for applying the "content" filters to some bit of data.  Typically, this is so that the text can be formatted with things like curly quotes and paragraph tags.

This is not the way to do it:

	$text = apply_filters( 'the_content', $text );

WordPress expects this filter hook to be called within The Loop context.

Mark Jaquith, one of the lead developers for WordPress, has [this to say on the subject](https://core.trac.wordpress.org/ticket/24330#comment:3):

> WordPress core has, for years, relied on the convention that `the_content` filters are meant to be run inside a loop context with a valid global `$post` object. Multiple WordPress core functions already make that assumption, like `gallery_shortcode()` and `prepend_attachment()`, as well as all our embed handlers (which do caching by post ID). Any third party shortcode that touches post meta will be in the same boat, and won't work if `$post` isn't as expected.
>
> It's not very clean, but it is expected and well-established behavior.

Suffice it to say, the above code breaks plugins that filter `the_content` but rely on the global `$post`.  Not to mention, all kinds of plugins filter the content.  There's no telling what your users might have show up in some text unrelated to posts.

## How to do it

If you just want "the content" filters, roll your own filter hook like so:

	$text = apply_filters( 'th_awesome_text', $text );

Then, apply your preferred filters:

	add_filter( 'th_awesome_text', 'wptexturize'       );
	add_filter( 'th_awesome_text', 'convert_smilies'   );
	add_filter( 'th_awesome_text', 'convert_chars'     );
	add_filter( 'th_awesome_text', 'wpautop'           );
	add_filter( 'th_awesome_text', 'shortcode_unautop' );
	add_filter( 'th_awesome_text', 'do_shortcode'      );

Pretty simple stuff. You can mix and match those, add other filters, or do whatever you want with that.  By using a custom filter hook, you have far more freedom and won't run into any type of conflicts.
