<a href="http://themehybrid.com/hybrid-core"><img src="http://themehybrid.com/blog/wp-content/uploads/2014/07/hybrid-core-tall.png" alt="Hybrid Core screenshot" width="350" height="812" class="alignright size-full wp-image-2431" /></a>

[Hybrid Core](http://themehybrid.com/hybrid-core) 2.0 has been a long time coming.  This is only the second time that we've had a major release of the framework, which is one of the reasons it took a while to get things ironed out.

I feel like I could've worked on 2.0 for another few months, adding more awesomeness here and there.  But, at a certain point, you just have to stop building and say, "This is where the code is at. Let's release it."

This version of the framework has been at a stable point for a long while now, as evidenced by the many people who have been using it (including myself) for a few months.  

Frankly, it's time to ship the thing and start work on the ideas that didn't quite make the cut for this release.

## Why version 2.0? ##

If you're wondering why version 1.7 was skipped, it's because Hybrid Core doesn't follow WordPress' versioning system, which technically doesn't have major releases.  Rather, the framework follows [Semantic Versioning](http://semver.org).

Because this version of Hybrid Core is dropping a lot of backwards compatibility, the version number was changed to 2.0 (or 2.0.0).

## What has changed in 2.0? ##

If I listed every detail, or even most details, this might be one of the longest blog posts ever written.  This version had over 200 code commits by several people, so it'd be a lot of ground to cover.  If you're interested in looking through them all, check out the [commit log](https://github.com/justintadlock/hybrid-core/commits/2.0.0).

What I'm going to do is tell you all about the things that interest me the most.

### Composer support

[Composer](https://getcomposer.org/) is a PHP dependency manager.  As far as I know, Hybrid Core is the first  theme framework to include support for it (there may be others though).  I'm not particularly familiar with working with Composer, but Andrey Savchenko, better known as [Rarst](https://twitter.com/Rarst), is.  He pioneered this feature for Hybrid Core.

For many of you, this might not be a big deal, but this will be helpful for those of you who need it now or in the future.  Plus, I wanted to make sure Rarst got a bit of acknowledgment for his work on this and for teaching me a thing or two.

Here's the [package link](https://packagist.org/packages/justintadlock/hybrid-core) on Packagist for those of you who need it.

### Out with the old

Like I wrote earlier, Hybrid Core 2.0 dropped a lot of legacy code.  I didn't want us to continue building bloat like other frameworks.  One of the goals of the Hybrid Core framework has always been to remain lean.

A couple of the major things that were dropped were things that we already had in plugin form.  [All widgets were removed](http://themehybrid.com/weblog/where-oh-where-have-my-widgets-gone) in favor of the [Widgets Reloaded](http://themehybrid.com/plugins/widgets-reloaded) plugin.  Please encourage your users to download this plugin if they want to keep the widgets.  The Entry Views extension was also [converted into a plugin](http://themehybrid.com/weblog/entry-views-wordpress-plugin).

The Custom Field Series, Theme Fonts, and Color Palette extensions were dropped.  Custom Field Series has long been deprecated.  I encourage those of you who have still been using it to check out my [Series plugin](http://wordpress.org/plugins/series).  The Theme Fonts and Color Palette extensions never panned out.  I'll most likely be setting up separate projects for these for anyone who still needs them or wants to help improve the code.

All deprecated functions prior to 2.0 have been permanently removed.  

Post and comment-related template shortcodes were also removed. For some theme developers, this may present a bigger hurdle to jump than some of the other items if you were making use of them.  I'll be more than happy to help with anything you need to do to transition your code.

### Attributes system

Hybrid Core had body, post, and comment classes long before these were added to WordPress core.  When WP added these, they didn't really innovate and push the feature where it needed to go.  Therefore, I decided to build us a new HTML attribute system directly in the framework.  Rather than using `body_class()`, for example, you'd use something like this:

	hybrid_attr( 'body' );

This allows us to tack on any number of attributes to the `<body>` element and not just classes.  This is a major improvement because it helps us on a number of fronts:

* Infinitely flexible. It can be used for any HTML element and any attributes.
* Built-in support for [Schema.org microdata](http://schema.org).
* Built-in support for Accessible Rich Internet Applications (ARIA).
* Compatibility with the WordPress `body_class`, `post_class`, and `comment_class` hooks to keep plugin authors happy.

Hybrid Core has a number of predefined elements plus attributes in this system, but you can also create your own.

Hat tip to [Andrew Norcross](http://andrewnorcross.com) and [Ryan Van Etten](http://ryanve.com/) for the [original ideas](https://github.com/justintadlock/hybrid-core/issues/17) on what would eventually become this feature.

### Template tags

The framework has always had template tags, but they were a bit scattered throughout the files.  Version 2.0 introduced new files in the `/functions` folder for template tags.  You'll quickly notice them because each file has a name of `template-*.php`.

There are many new template tags for you to use.  Most of them are on my WordPress "wish list," so I hope to eventually see them added to core WordPress.  They are functions that I believe are hugely beneficial to theme authors.

### Even better global support

We've made great strides in beefing up support for developing translation-friendly themes.  The first major improvement was to re-code a nasty hack to get the framework translations into the theme.  This issue has been solved, which also has the benefit of huge speed increases for everyone.

There are also a couple of extra functions for getting the language and region of a user's WP install.  You could do some cool things with these.

My favorite new feature though has to be the new locale stylesheet system, which improves upon what WordPress already has in place.  Now, there's a clear hierarchy for custom stylesheets.  For example, the hierarchy for Korean would be (loaded in addition to the theme's `style.css`):

* Locale: `css/ko-kr.css`
* Language: `css/kr.css`
* Region: `css/ko.css`
* Text Direction: `css/ltr.css`

## The tip of the iceberg

I wish I had the time to write about all the new features and changes within the framework. I'm excited about each of them because it represents a major shift in how we'll be coding themes in the future.

If you'd like to check out some themes that are already running on version 2.0 to see how they work, check out:

* [Stargazer](http://themehybrid.com/themes/stargazer)
* [Socially Awkward](http://themehybrid.com/themes/socially-awkward)
* [Ravel](http://themehybrid.com/themes/ravel)

I'll be working on updating documentation as soon as I can, but it's going to take a little time to document everything fully with this change.  Don't hesitate to open a new support topic in the meantime.  Support topics actually help me write better documentation because I learn what it is you all need to know.

## Download version 2.0

You can grab the latest version from the following links:

* [Hybrid Core page](http://themehybrid.com/hybrid-core)
* [GitHub repository](https://github.com/justintadlock/hybrid-core)