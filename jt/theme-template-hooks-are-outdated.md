# Theme template hooks are outdated

9/16/2013 12:18:58 PM 

*[API]: Application Programming Interface
*[CSS]: Cascading Style Sheets
*[HTML]: Hypertext Markup Language

Believe it or not, there was a time when child themes were only a `style.css` and `screenshot.png` file.  It wasn't until [August 2006](http://core.trac.wordpress.org/changeset/4131) when they were allowed to have a `functions.php` file.

We wouldn't see the ability for child themes to have their own templates until two years later when Ian Stewart opened one of the most important WordPress [Trac tickets](http://core.trac.wordpress.org/ticket/7086) in the history of theming.  Some of you may even remember the days when the only way to achieve this feat was with a plugin coded by [Kristin Wangen](http://thewangens.net/).  *Those were the days, right?*

These two changes marked vitally important points in history that drastically changed the landscape of WordPress theme design.

## How template hooks became common

Back in 2008, Ian Stewart had the [Thematic](http://wordpress.org/themes/thematic) theme and I had the [Hybrid](http://themehybrid.com/themes/hybrid) theme.  There was also [Sandbox](http://wordpress.org/themes/sandbox), the theme from which these two theme concepts derived.  Thematic and Hybrid were the two big players in the community when it came to child themes.  It was a concept that few people knew about.  Sandbox had made it popular with some designers, but Thematic and Hybrid made it popular with many more 1,000s of users.

It took a while to grok the idea of child themes for many, but people were flocking to these two themes.

The ideas behind the child theme concept were:

* You could upgrade your parent theme without losing your modifications.
* You could create many different designs without writing the markup.

Users want to make theme modifications.  Everyone wants their own personal touch to their site.  But, child themes were limited at the time.  You were only allowed a `style.css`, `functions.php`, and `screenshot.png` file.

This is where template hooks became extremely useful.  Both Thematic and Hybrid allowed you to hook in at various places and insert whatever content you wanted (action hooks) or overwrite existing content (filter hooks).  You could do this with a little bit of code in your child theme's `functions.php`.  The idea was brilliant.  It was so brilliant that other theme authors caught on.  The practice still exists today to the point of being commonplace.

Here's the problem though:  *What are hooks? What's a `functions.php` file?  Oops, my whole site just went blank!*

A theme's `functions.php` file is dangerous territory for your average user.  Hooks are part of the [Plugin API](http://codex.wordpress.org/Plugin_API).  They were created for plugins to hook into various parts of WordPress and do cool stuff.  It's no place for Jimmy Joe to be messing around in.

We needed something better.

## Overwriting templates

I mention Ian Stewart's ticket as being the most important change to WordPress theming ever.  That made it possible to overwrite templates in child themes, which makes a lot more sense to average users.  HTML and a few template tags are a lot easier to deal with than the complexities of hooks.

This change was not without its drawbacks.  Overwriting an entire template for a minor change in the posts loop wasn't that useful.  It was still better to use a hook for minor adjustments.

This brings me to the second most important change in theming history: the introduction of [template parts](http://core.trac.wordpress.org/changeset/13146) (note the function named was later changed to `get_template_part()`).  Template parts are a method of breaking a larger template down into smaller parts.

We had already been using template parts for headers, footers, and sidebars for some time.  This change gave theme authors the ability to create custom template parts that theme users could overwrite in their child themes.

## Making template hooks irrelevant

There has been a push to get a set of [standard template hooks](http://core.trac.wordpress.org/ticket/21506) into WordPress core for a while.  The problem with that is the adoption rate by theme authors and that all themes are coded a bit differently.

I question whether this enhancement to WordPress is useful anymore for two reasons:

* With the introduction of template parts, child theme users can more easily make modifications.
* Plugins really don't need many more hooks (more on this below).

In the past year or so, I've been making major changes to themes at [Theme Hybrid](http://themehybrid.com).  I'm starting to build themes without template hooks.  Yes, one of the guys who pioneered this movement is now pulling out.  I'm breaking down my templates into smaller parts because:

* I can cut back on some duplicated code.
* I can create context-specific sections of code.
* Users can digest minor bits of HTML and template tags better.

After 5 years of support questions, it's finally sinking in &mdash; users understand HTML and template tags better than their `functions.php` file.  

It's much simpler for me to say, copy `breadcrumbs.php` into your child theme and do this than to say `add_action( 'hook_name', 'your_func' )`, `functions.php`, etc.  One is easier than the other.

My advice to theme authors is to start rethinking your use of hooks.  This is not to say that all theme hooks are useless.  Hooks are a powerful feature and useful for many things.

## Giving plugins some love

There are areas in themes where plugin authors have needed hooks for years, particularly areas surrounding posts and comments.  Hooking into these two areas has been notoriously wrought with issues.

I'm all for adding in a few extra hooks to make plugin authors' lives easier.  Plus, with the WordPress.org theme review process, we can make sure theme authors adopt these new hooks in any theme coming through our system in a reasonable amount of time (we already do this for the `wp_head` and `wp_footer` hooks).

However, right now, I can't get behind a project where we're adding in a ton of new template hooks, not when the problem template hooks were meant to solve can now be solved with smarter template logic.  Also, I have [a method](http://core.trac.wordpress.org/ticket/21506#comment:63) that would allow WordPress to auto-create additional hooks when using template parts.