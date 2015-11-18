# Misconceptions about the Hybrid Core framework

Yesterday, WPMU DEV [published an article](http://premium.wpmudev.org/blog/choosing-a-wordpress-theme-framework-the-ultimate-guide/ "Choosing a WordPress Theme Framework – the Ultimate Guide") on WordPress theme frameworks, calling it the ultimate guide to choosing one.  I was happy to find that my own [Hybrid Core Framework](http://themehybrid.com/hybrid-core) was listed among some great projects.  It even garnered some nice scores in the rankings (overall score of 4/5 stars).

It's always nice to see that others appreciate and recognize your hard work.  It's also tough to do full and thorough reviews with comparisons.  This post isn't about knocking the work that Rachel McCollin (the author) put into the post.  I know it's hard to get everything right.

However, there were a number of errors that I wanted to correct about Hybrid Core and frameworks in general.  Because I can't comment on the article without a social network login or signing up for their site, I decided to write an article myself.  My hope is that this will be beneficial to anyone looking to use Hybrid Core in the future.

## What is a theme framework?

This is my gripe with not just this particular article but many that I see around the Web.  As defined in the WPMU DEV article, frameworks are:

> Frameworks are designed to work as parent themes, which means that when using one to build a site, you'd normally use a child theme.

Well, this is not exactly correct.  It's actually the third (in a list of three) definition of frameworks on the official [WordPress Codex page](http://codex.wordpress.org/Theme_Frameworks) on theme frameworks.

Hybrid Core doesn't fit into this category at all.  It's under the first definition of theme framework:

> A "drop-in" code library that is used to facilitate development of a Theme.

The WPMU DEV article seems to disagree with this definition.  Its article goes on to say that this isn't a framework yet added Hybrid Core, a drop-in framework, to its list (see the section on "Code Libraries").

Hybrid Core was designed specifically to drop into any theme.  It also facilitates the use of child themes.  However, it is not a theme in and of itself.  If you're interested in finding out more on this particular subject, I recommend reading my [article on frameworks](http://justintadlock.com/archives/2010/08/16/frameworks-parent-child-and-grandchild-themes).

## It's "Hybrid Core"

While we often use the term "Hybrid" to refer to the framework at my site in general discussion, its name is actually "Hybrid Core".  That's just a little pet-peeve of mine.

## Dashboard vs. Admin

The article mentions "dashboard" many times.  However, the correct term for what was written is "admin".  The dashboard is but one screen in the entire WordPress admin.

This is an important distinction.  Any theme, plugin, or framework can have dashboard options and/or other options and so on throughout the admin.  Generally speaking, most WordPress themes and theme frameworks shouldn't have anything in the dashboard.  It usually doesn't make sense to do so.  Most of the time, such things would be plugin territory.

Mostly, I want to clear up the terms "dashboard" and "admin" because I'll be writing about those below.

## Library of child themes

In the "good" column for Hybrid Core, the author listed "Growing library of free child themes (33 at time of writing)" as a positive for the framework.  It's great that I got some positive points there, but it's also completely incorrect.  There is no such thing as a child theme for Hybrid Core.  It's not a theme.  Therefore, it cannot have child themes.

[Theme Hybrid](http://themehybrid.com) (my site) does have a number of [parent] themes built with the Hybrid Core framework.  Some of those themes also have children.  However, there are many more themes out there in the wild built with Hybrid Core on such sites as [DevPress](http://devpress.com), [ThemeForest](http://themeforest.net), [WordPress.org Themes](http://wordpress.org/themes), and many others.

## Limited admin options

The article describes Hybrid Core as having "Limited dashboard [sic] options".  I suppose that could be true, depending on how you look at it.  Out of the box, with no features enabled, it has zero admin options.

However, Hybrid Core is a modular framework.  Only the options enabled by the theme developer will be used.  Depending on which options are available, there are a number of admin options that may be used by the eventual theme user.  Some of these options are theme layouts (global and per-post), per-post templates, and per-post stylesheets.  If you're a theme author, those three options almost open up limitless possibilities for building themes, particularly when you have sites with dynamic designs that change depending on what page you're on.

It's also worth noting that Hybrid Core has a wrapper for the WordPress Settings API.  This is so developers can more quickly add theme options if they wish to do so.  I do discourage this though and try to push theme authors into building things with WordPress' built-in customizer.  Hybrid Core also has some extra developer-friendly classes for working with the customizer.

## Large number of template files and includes

One of the other cons listed in the article is "Large number of template files and includes - can take time to get to grips with".  While there are a number of includes, there are absolutely no template files in Hybrid Core.

Zero.  None.  Zilch. 

Again, Hybrid Core is not a theme.  It does not have template files.  I'm also not sure why this was listed as a negative for Hybrid Core.  It actually has far fewer files than some of the other frameworks.

## For non-coders

Hybrid Core was given 3/5 stars in the rating "for non-coders".  That is extremely generous.  I would've given it 0/5 stars, and I'm the framework author.

Hybrid Core in the hands of a non-coder is not such a good idea.  It's a framework.  By that very definition, it is meant for programmers, not users.  There'd be no reason ever for a user to be messing around with it.

Like I mentioned earlier, there are many themes built with Hybrid Core.  Those themes are built for non-coders.  The framework?  Not so much.

## &lt;/rant>

I was mostly just having a little fun and trying to clear up a few things at the same time.  Many of these things are common errors found in many articles on the subject, so it does get a little frustrating at times when I'm reading through them.

Thanks to Rachel for listing Hybrid Core in her article and giving it high marks.