Just over [four years ago](http://justintadlock.com/archives/2010/07/16/a-wordpress-forum-plugin-using-custom-post-types), I built a forum plugin using WordPress' fairly new API for post types.  At the time, the bbPress plugin didn't exist.  The development of the original bbPress software (not plugin) had come to a grinding halt.  I needed something that would work for a couple of clients who needed a simple solution.

The original plan was to continue working on this plugin and release it into the wild.  There was certainly a lot of interest from people who wanted a forum on their site.  That never happened.  I thought the best thing to do would be to step aside and allow bbPress to flourish.  Frankly, I didn't want the job of leading a project like a forum plugin at the time because I felt like it would interfere with everything else I had going on.

Now, I'm ready for the project.  In fact, the [support forum](http://themehybrid.com/board) here at Theme Hybrid has now been switched over to this new plugin.  This is one surefire way to make sure I devote the time and energy to keeping the plugin alive.  Because it runs the **most important** part of my site, it's continued development is critical.

## Why not bbPress?

That's the million-dollar question, right?  I don't want to spend too much time answering this over and over, so I'll try to explain the decision here and now.

I loved the original bbPress software.  Until last night, I had been using a customized version of it on this site for the past 6 years.  It's what forum software should be &mdash; lightweight and infinitely extendable via plugins.  This software has been dead for the last 5 of those 6 years, and I didn't think it was a good investment of my time to continue development with it for just this site.  Plus, other than the user tables in the database, it was completely separate from my WP install, which means there are a number of issues and hurdles to overcome.

The bbPress plugin looked awesome from the onset.  I had some concerns about how some things were handled, but I knew they had to be done that way because of limitations that existed within WordPress (many of which still do exist).

I've kept an eye on bbPress development over the years.  While I haven't looked at it much in the past year in detail, I don't see the project headed in the direction that suits me, which is perfectly OK.  I'm only one person in comparison to the project's entire user base.  It doesn't fit my development style.  The plugin tries to do too much (like the theme compatibility and shortcodes system).

I've got mad respect for the folks who work on the bbPress plugin, but it's simply not for me.  I also believe it is healthy for the ecosystem to have competing plugins in the same space.

## About my plugin

First and foremost, this plugin is a solution for Theme Hybrid.  At this stage, development is going to be largely focused on building a plugin that I'm happy with using on this site.  I do a lot of *cowboy coding* and will make large and drastic changes on projects to suit my needs.  Of course, this is how nearly every one of my plugins are initially created.

I just want to be clear about that upfront.

With that said, I would like to see this turn into a great forum solution for the WordPress community.  The goals of the plugin are:

* Be as lightweight as possible.
* Offer the bare essentials for running a forum.
* Focus on tools for developers more than features for users.
* Allow plugins to extend it for user features.

If you are interested in following or even helping out with this project, you can do so from its [GitHub repository](https://github.com/justintadlock/message-board).  It is in an early alpha stage, the code is all over the place, and it should not be used on a live site unless you're a developer who knows what he's doing.