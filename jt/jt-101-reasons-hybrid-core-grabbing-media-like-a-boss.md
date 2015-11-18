# Grabbing media like a boss

<img src="http://justintadlock.com/blog/wp-content/uploads/2014/07/s-awkward-video-screen-960x943.jpg" alt="Video post in the Socially Awkward WordPress theme" width="900" height="884" class="size-large wp-image-5515 aligncenter" />

Now that Hybrid Core version 2.0 has been [officially released](http://themehybrid.com/weblog/hybrid-core-version-2-0), I thought it'd be a good idea to continue this series of posts highlighting cool stuff from [the framework](http://themehybrid.com/hybrid-core).

In this post, I want to introduce you to a feature we call the "Hybrid Media Grabber" because it can be pretty useful for theme authors who want to do awesome stuff with media.

## An idea was born

Way back when I was a partner at [DevPress](http://devpress.com), Tung Do had this awesome design (like he always has).  Unfortunately, there were parts of it that none of us on our team really had the skill level to code without making it hard for the user and not portable to other themes.

*Does this sound familiar to any other developers?  Yeah, those pesky designers don't know the limitations of the software.*

What we needed was an easy way to get a video (YouTube, Vimeo, self-hosted, etc.) for a post and put it wherever we needed it for the theme's design.  That's a bit of problem for a couple of reasons:

* We could use custom fields, but that wouldn't be portable to other themes.
* The user could stick it in the content, but that'd make it hard to get out.

After our team parted ways, this idea stuck with me.  I also found that I needed it for one of my own projects later.  

Eventually, WordPress got lots of new stuff for working with media, which made this idea look a lot more realistic.  I was motivated to get this thing done and first used it in [Socially Awkward](http://themehybrid.com/themes/socially-awkward), a media-focused WordPress theme.

## What does the media grabber do?

Well, it grabs media.

More precisely, it grabs media related to a post.  It first looks within a post's content for media that's been added by the user.  If no media is found, it'll look for media attached to the post.

The ability to do this is cool for a couple of reasons:

* You can get a post's media without showing the full post content.
	* Use it in a widget.
	* Show it alongside excerpts on archive-type views.
* You can split this media from the post content on single post views.
	* Show it above the content.
	* Show it somewhere else on the page.

It's the audio/video equivalent of featured images, which has a lot of potential.  *Video theme, anyone?*

The feature supports a lot of different methods of adding media that the user might have used:

* Plain ol' HTML `<video>`, `<iframe>`, and `<object>` tags.
* <code>&#91;embed]</code> shortcode.
* WordPress auto-embeds.
* <code>&#91;audio]</code> and <code>&#91;video]</code> shortcodes for self-hosted media.
* The Jetpack plugin's audio/video shortcodes.
* Attached media files.

## What does the future hold?

Right now, the media grabber only supports audio and video.  However, I could easily see the day when other types of media are supported.

I'm also willing to work with plugin authors who have custom shortcodes for adding media.  Jetpack integration was phase one.  It'd be nice to integrate with other plugins too.