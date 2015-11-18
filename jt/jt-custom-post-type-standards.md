# Custom post type standards

There has been some talk recently of setting some standards for custom post types in the WordPress community.  Actually, this has been an ongoing discussion for a few years.  I think I've [made it clear](http://justintadlock.com/archives/2013/09/14/why-custom-post-types-belong-in-plugins "Why custom post types belong in plugins") that I'm a fan of this idea.  So, I wanted to present my take on this discussion.

I also want to expand on this a bit because this is something I've been preaching for years.  However, I don't think I've ever explained what I mean completely.

## What can we standardize?

When most people talk about standardizing custom post types, what they're usually referring to is standardizing on a post type name.  That's a good start because WordPress stores this in the `post_type` field for a post.  Therefore, a post is directly tied to its type. 

It makes sense to have some standards on some common post types.  Here's a few:

* `testimonial`
* `portfolio_item`
* `recipe`
* `faq`
* `event`
* `product`

That's a really, really good idea, right?  Let's standardize on some post type names so that there's at least some portability between different plugins.  It's fairly easy to create a working group of standard names.  An official page on the WordPress Codex wouldn't hurt.

However, I'd argue that a little common sense also goes a long way.  If you're making an "events" plugin, don't name your post type `justin_event`.  Name it `event`.  This isn't really brain surgery, and I don't think the WordPress developer community needs that much hand-holding to figure this out.  But, if we do, let's start that Codex page.

The only reason for any type of standards for post type names is so that it helps foster healthy competition between various plugins trying to fill the same space.  This is so users can more easily switch between plugins to find the one they like the best.

## We've been talking about the wrong problem.

While naming standards have been a problem, that's not that big of a [hurdle to overcome](https://wordpress.org/plugins/post-type-switcher "Custom Post Type Switcher").  That's not the problem anyway.  Brian Krogsgard explains the big problem perfectly in his [article on post type standards](http://www.poststat.us/wordpress-com-jetpack-lead-way-toward-standardizing-custom-post-types):

> For years we've been talking about the importance of not "locking in" users to CPTs bundled with themes. At some point, that gained decent adoption, but people still tended to just package the same code that was in their theme and put it in a separate plugin &mdash; a fine practice for sure. But it's not a practice that makes it much easier to go from one portfolio theme to another &hellip;

People are still using their own, separate code rather than adopting existing solutions, preferring a solution built in-house instead of joining together with others.  That's the reason we don't have standards.  It really has little to do with post type naming conventions.

Standards are created after we've made them and they've been adopted by enough people.  In other words, we create standards by building good plugins, getting users to install them, and having theme authors integrate with them.

## A look at a standard that exists.

I want to provide a real-world example of an existing standard so that I can fully explain my meaning.  

If you're doing anything with e-commerce and WordPress right now, you're either using [WooCommerce](http://wordpress.org/plugins/woocommerce/) or you at least took a long and hard look at it before deciding on a different solution.  WooCommerce is **the** standard for e-commerce in the WordPress community.  I don't think anyone can argue that point.

Why is it the standard?  Well, it's got a whole heck of a lot of users and a wide adoption rate by theme authors who are building themes for it.  That pretty much makes it the standard.

Does anyone know what the post type name is (I didn't before writing this post)?  Not that it really matters since they've established the standard in this space, but the main post type used is `product`.  That fits right in with my common sense approach mentioned earlier for naming standards.  If you're a plugin developer who wants to compete in this space, you sure as hell better name your "product" post type `product` and follow all the other standards that WooCommerce has already established (post types, metadata, taxonomies, etc.).

Here's the thing about post types though.  They're not really about registration (i.e., naming them).  Post types are about implementation.  What I mean by this is that we create standards by building the best plugin for the specific scenario.  We can talk in circles about proper names all we want, but it's not really getting down to the point.

## Now, let's get to the real point.

It's not really about post types is it?  Take a moment and think about it.  Think about WooCommerce for a moment.  Do you really care what post types it creates? 

No.  I didn't think so.

What matters is building solutions.  They've got a solution that works as evidenced by both the user and developer community around the plugin.

Ask a single non-developer WooCommerce user if they care at all about this discussion.

## Shameless self-promotion

Hey, it's my blog, so I'm going to point out my own plugins.  Here's a few solutions I'm working on.  I'd love to get both plugin and theme developers on board these projects to help make them more of a standard in the WordPress community.

* [Whistles](http://wordpress.org/plugins/whistles) ([GitHub](https://github.com/justintadlock/whistles)) - Tabs, toggles, and other fancy bells-and-whistles. (need UI/UX developers).
* [Custom Content Portfolio](http://wordpress.org/plugins/custom-content-portfolio) ([GitHub](https://github.com/justintadlock/custom-content-portfolio)) - Portfolios (could use input from theme authors).
* [Restaurant](http://wordpress.org/plugins/restaurant) ([GitHub](https://github.com/justintadlock/restaurant)) - Restaurant management (lots of room for add-on plugins; definitely commercial plugin potential).

I've also got a few other projects in the pipeline.  The only way these upcoming projects and those listed above will gain any traction is by use.  What good is a Restaurant plugin if no one is building themes that will beautifully display the food menu items?

You want standards?  Help me out.  Help each other out.  Let's join together and build cool stuff.