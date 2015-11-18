# Why custom post types belong in plugins

9/14/2013 2:32:37 PM 

*[API]: Application Programming Interface
*[CSS]: Cascading Style Sheets

<p class="alert">Just to be clear before continuing, this article specifically deals with publicly-distributed themes and plugins, whether free or commercial.  It may not apply to some custom work.  What's best for your client will have to be decided on a case-by-case basis.</p>

I and others in the WordPress community talk a lot about putting custom post types, taxonomy, and content-generation features into plugins.  We say it's not a good idea to put this stuff into your theme.  However, it recently occurred to me that the reasons for this are rarely explained in full detail.

This article will primarily focus on custom post types because they're so prevalent in "premium" themes, but it's really about any features/functions that can be used to create content.

## What is a "content-generation" feature?

Essentially, anything that a user can use to create content falls into this category.  The following is a list of some examples.

* Custom post types.
* Custom taxonomies.
* Custom database tables.
* Custom shortcodes.
* Custom comment types.

If a user is creating some type of content or data on their site, they're using some type of content-generation feature or tool.

## Why users should be concerned

The first part of this article will focus on user concerns.  If you're a WordPress user, these are things you'll need to take into consideration.

### The lock-in problem

I've previously written about the lock-in problem in a [post on shortcodes](http://justintadlock.com/archives/2011/05/02/dealing-with-shortcode-madness "Dealing with shortcode madness").  The lock-in problem is when a user is forced to continue using a theme because their data would be lost to them if they switched to another theme.

Let's face it.  User's switch themes.  That's the beauty of the WordPress theme and plugin system.  A user can continue using the same plugins (functionality) and switch themes (presentation) daily if they want to.

If a user can only create certain types of content or loses access to that content after switching to another theme, that's a major problem.

This is also a loss of functionality.  Some post types have functionality tied to them, not just content.  So, you might lose access to both your data and specific functionality that you had before.

### Data portability

When custom post types were first introduced, it was an awesome time to be involved with WordPress.  I even wrote one of the most popular [tutorials on post types](http://justintadlock.com/archives/2010/04/29/custom-post-types-in-wordpress "Custom post types in WordPress").  Unfortunately, many people have used that tutorial to do more harm than good.

Custom post types in WordPress gave us a way to create custom types of *content*.  There's that word again &mdash; content.

Let's suppose for a moment that your theme created a custom post type with the name of <code>portfolio_item</code> so that it could allow you to build a portfolio of your work.  This seems harmless enough, right?  It actually sounds like a good thing.

The reason it's not a good thing is because your data is now tied to your theme.  It is not portable.

When we talk about "data portability" in the WordPress community, we're primarily talking about being able to keep and access your data regardless of the theme you're using.

*What happens when you switch to a theme without the same, exact post type defined?*  Suddenly, you can no longer access your portfolio.  It doesn't show on your site.  Your portfolio items aren't in the admin.  They simply disappeared.

Granted, the data still exists in your database.  You just can't get to it without the proper WordPress functions.

### Recreating content

Let's suppose you did find another theme that had a portfolio post type after switching from the old one.  You might think that it would allow you to use your data.  That may or may not be true.  It actually depends on the post type name. 

In the example above, I used `portfolio_item` as the name.  However, another theme might define that as `portfolio`.  If those names don't match, you must recreate each of your portfolio items if you wish to continue displaying your portfolio and using this new theme.

### What you can do as users

You may be thinking as a user that you have no control over this.  You actually do.  Any good theme author listens to questions and feedback.

If you're purchasing a commercial theme, be sure to find out if you'll lose your data when switching themes before you make your purchase.  Find out what plugins the theme supports or suggest plugins to the theme author.

It just seems a little crazy to me to spend $50 or more on a theme only to find out a while later that all your hard work has disappeared when you switched to another theme.

## Theme authors

Obviously, this post is focused on themes.  In this section of the article, I hope to explain the reasons you should stop adding post types to your themes and give you alternatives.

### Separating function from form

WordPress has two systems for extending the platform:

* Plugins
* Themes

Plugins are meant to be installed on a site and provide functionality that can be used with, essentially, any WordPress install.  They hook in their own functions using the plugin API and "do stuff".  Plugins have few limitations on what they can do.

Themes, on the other hand, are limited in comparison to plugins.  Their purpose is to handle the presentation of the user's data.  They have a fairly strict set of rules they should follow because they need to conform to certain conventions in order to properly present that data.

*Are there times when the line between theme and plugin functionality gets blurred?*  Certainly.  There's no denying that.  However, I've rarely seen a case where that line wasn't clear when it comes to generating content.

### Reasons to put your custom post types in a plugin

I'll just list off a few:

* **User concerns:**  For all the reasons I covered above about users.
* **Code re-use:**  If you decide to make another theme in the future with the same post type, you then have to maintain code in two (or more) places.  If you place it in a plugin, you have only one set of code to worry about.  Any good programmer knows it smarter to have it in one place.  This is like Programming 101.
* **Playing nice:**  Wouldn't it be great if other theme authors could build themes using your plugin?  That just makes you more famous and popular in the WordPress community.
* **More users:**  Providing a plugin will provide another avenue for users to find your theme work.  This is free marketing for your themes.
* **You're a designer:**  There are some people who do both design and dev work, but most theme authors lean toward the design side of things.  Why put all the effort into programming when you could be designing?

### Examples to follow

One of the things I envision for the future of WordPress is a trusted set of plugins that define standards for post types and related data.  The idea is that if you wanted to build a portfolio theme, you'd design for the most popular portfolio plugin.  Or, if you wanted to build a restaurant theme, you'd choose the best restaurant plugin to design for.

Plugins like bbPress, BuddyPress, Jigoshop, WooCommerce, and others have already been paving this path.

When was the last time you designed a theme with built-in post types for forums, forum topics, and forum replies?  Most likely, you've never done that.  You simply added some templates and created some custom CSS for the bbPress plugin.

Are you building an entire e-commerce solution in your theme?  I didn't think so.  You're designing for Jigoshop or WooCommerce.

Why is it that you're adding other post types to themes but not those?  It might be for lack of a standard community plugin.  If that's the case, why are you not building that plugin and setting the standard?

### What good is data without the theme to present it?

This is a valid question.  Again, I'd really like to point out the plugins above as fine examples that answer that question.

Realistically, you need a theme that was specifically designed for a plugin to present the data in a beautiful way.  But, if more theme authors start using and backing specific plugins, users will gain more choices rather than being stuck.

Let's look at my [portfolio plugin](http://wordpress.org/plugins/custom-content-portfolio "WordPress Plugin: Custom Content Portfolio") as an example.  At the moment, it's not that popular.  However, there are now several themes that support it.  Imagine if every "portfolio" theme for WordPress supported that plugin.  Users would have tons of theme choices.

What I'm trying to do with that plugin is set a community standard for portfolios.  Getting valid feedback on it from theme authors will help push that standard.  Oh, and you actually have to support it by designing your themes around it (a few templates and some CSS).

### Do you really need a post type for that?

I'm not entirely sure that my main example, portfolios, should qualify for their own post type.  I see a case being made either way.  One thing I ask you to consider as a theme author is if you even need a post type to do what you need to do.

Consider the `portfolio_item` post type.  For many of the themes I've seen with this, all they really need is a custom page template that pulls in "image" (post format) posts.

Just give it a little thought.  Consider if a post type is truly necessary first.

## Edge cases

I'd like to take a moment and say that I do think there are use cases where these rules don't strictly apply.  With that said, this is usually not what I see in most themes.

If you think you have a good reason for adding a custom post type to a theme, I can probably give you a reason not to.  Actually, I've probably already covered it above.

## Questions/Comments

Feel free to ask me any questions about overcoming any development hurdles from a plugin or theme author standpoint.  I've done a lot of work with custom post types over the past few years.  I've done some of the greatest things and made some of the dumbest mistakes you can do with them.

If you're here to just complain about "how that's impossible", then there's little point in commenting.  I've heard it all before.  If you think something is impossible but are willing to work with me, I'll be glad to discuss it with you.