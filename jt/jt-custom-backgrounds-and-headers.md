*[CSS]: Cascading Style Sheets

*What? You don't like my spiffy header image and background on this page?*

So, I didn't have the time to make a cool design for this blog post because I've been hard at work putting together two new plugins for you all.  Not to mention, I had to re-code some of the stuff in my theme to actually use the WordPress custom background and header features.  These two plugins allow you to create either per-post backgrounds or headers.

I was watching a video, [(What's So Funny 'Bout) Themes, Love, and Understanding](http://wordpress.tv/2013/08/10/ian-stewart-whats-so-funny-bout-themes-love-and-understanding/), by Ian Stewart the other day.  Every time I watch one of his presentations, it always helps me to remember to have a little fun once in a while with theme design.  This prompted me to finish these two plugins that integrate with any WordPress theme that supports WordPress' custom background and header features.

I've also always been interested in "art direction" on blogs.  Two of my favorite art-directed blogs are [Jason Santa Maria](http://jasonsantamaria.com/articles/) and [Gregory Wood](http://journal.gregorywood.co.uk/).  Basically, the idea is that you can have a custom design on a per-post basis.  This design would be specific to that post.  While the two plugins I'm releasing don't allow you full design control, they do give you something that's a little closer to that concept without having to write custom CSS.

Normally, I like to announce new plugins on my actual theme/plugin site, [Theme Hybrid](http://themehybrid.com), but that wouldn't have allowed me to show the plugins in real-world use.  Announcing them here on my personal blog gives me the flexibility of doing that.

## Custom Background Extended

<img src="http://justintadlock.com/blog/wp-content/uploads/2013/09/screenshot-3-960x425.png" alt="Custom Background Extended plugin" width="900" height="398" class="aligncenter size-large wp-image-5215" />

The Custom Background Extended plugin gives you the ability to create custom backgrounds on a per-post basis.  The plugin has several options:

* Add a custom background color.
* Upload a custom background image.
	* Background repeat setting.
	* Background position settings.
	* Background attachment setting.

You can find the plugin on [WordPress.org](http://wordpress.org/plugins/custom-background-extended) or [Theme Hybrid](http://themehybrid.com/plugins/custom-background-extended).

## Custom Header Extended

<img src="http://justintadlock.com/blog/wp-content/uploads/2013/09/screenshot-31.png" alt="Custom Header Extended plugin" width="800" height="368" class="aligncenter size-full wp-image-5216" />

The Custom Header Extended plugin allows you to create a custom header on a per-post basis.  This one's a little trickier than the backgrounds plugin because themes have such a wide range of header widths and heights.  It probably also requires a image resizing plugin when you switch themes.

The options this plugin gives you are:

* Upload a custom header image.
* Display/hide header text (if your theme supports this).
* Custom header text color (if your theme supports this).

You can find the plugin on [WordPress.org](http://wordpress.org/plugins/custom-header-extended) or [Theme Hybrid](http://themehybrid.com/plugins/custom-header-extended).

## Standards and conventions in themes

Some of you may wonder why I write so much about following specific standards when it comes to theme development.  These two plugins are perfect examples of why it's important to do so.

Both of these plugins require that your theme support the core WordPress implementation of either the [custom backgrounds](http://codex.wordpress.org/Custom_Backgrounds) or [custom headers](http://codex.wordpress.org/Custom_Headers) theme features.  If your theme is doing something else with custom backgrounds or headers, this plugin won't work.  Obviously, every theme doesn't support these features (nor should they), but themes that allow for custom backgrounds and headers should use the core WordPress features.

I know this isn't on the level of [post types in themes](http://justintadlock.com/archives/2013/09/14/why-custom-post-types-belong-in-plugins), but it's just an example of how themes and plugins can play nicely together when following established standards.

***

Enjoy the plugins!  

*Yes, I realize I just pushed us two steps closer to returning to the old Geocities days. All I need to do now is create a scrolling marquee and text blinking plugin and we're set.* 