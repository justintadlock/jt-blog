# Better front page preview

The front page shown in the WordPress.org theme previewer has been a subject of much debate.  There's some movement on getting better demo content, but the front page is the first impression.  We want it to look good and best represent what our themes are capable of.

Given the prevalence of non-blog themes, there needs to be a bit of balance here.  I've thought long and hard about what the best route would be for handling this.  The following is my proposal.  I'd like to get all of your feedback as well as check in with @otto42 on the feasibility of it before creating a ticket.

Let me know your thoughts.

<h2>How the front page should be shown</h2>

I wanted to keep this simple and make sure that it works with both regular blog themes and themes that have a custom <code>front-page.php</code>.

The previewer should have some code that checks:

* If <code>front-page.php</code> exists, override front page setting to show a page.
* Else, show regular blog posts.

<h2>The idea in code</h2>

Note:  This is potential code for the previewer to better describe my idea.  It's not something to put in your themes.

The following bit of code is a rough draft of how I think a feature should work.

<pre><code>&lt;?php

add_filter( 'pre_option_show_on_front', 'wptrt_show_on_front' );
add_filter( 'pre_option_page_on_front', 'wptrt_page_on_front' );

function wptrt_show_on_front( $show ) {

	return wptrt_has_front_page() ? 'page' : $show;
}

function wptrt_page_on_front( $page ) {

	// 100 is the page ID to show.
	return wptrt_has_front_page() ? 100 : $page;
}

function wptrt_has_front_page() {

	// Need a check to see if the current theme being previewed 
	// has a front-page.php template. If it does, return TRUE.
	// Else, return FALSE.

	return false;
}</code></pre>