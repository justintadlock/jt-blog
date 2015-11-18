# New membership plugins powering Theme Hybrid

Since I first launched this site in 2008, I've been using the same membership plugin.  Changing membership plugins is no small feat on a site.  There's tons that can go wrong.

Before I dive into this post, I want to apologize in advance if there are any hiccups in the next week or so as I iron out any problems.  Please do report anything to me via email, the support forums, our Slack channel, or even right in the comments on this post.

## Out with the old

In 2008, I bought my first "premium" plugin.

And, only about 10% of it actually worked.  

The only redeeming quality about the plugin is that it actually allowed me to get paid.  I won't mention the plugin I purchased at the time because I don't want to send the developers any type of traffic.  This isn't just because it was a bad plugin; it was the poor support experience as well.

Like I said, I could still get paid.  I just had to build all the membership stuff myself.

Fortunately, this led me to create my most popular plugin, [Members](http://themehybrid.com/plugins/members).  Of course, that plugin doesn't have a payment system built in.  

Between the purchased plugin, Members, and a lot of spaghetti code that I cowboy-pushed to my site over the years, I had something that sort of worked.

## In with the new

I pushed 4 new plugins, 1 plugin update, and deactivated the old plugin today.  Here's a list of the  new plugins if you're interested in what's running the site.

* [Easy Digital Downloads (EDD)](https://easydigitaldownloads.com) - The name says it all, really.
* [EDD Members](https://foxland.fi/downloads/edd-members/) - EDD add-on plugin for memberships by one of our own community members.
* [Role Map - EDD Members](https://github.com/justintadlock/role-map-edd-members) - Custom plugin I wrote to work with EDD Members and map user roles to the membership options.
* Theme Hybrid EDD - Custom plugin with minor EDD changes.

I decided to go with EDD for a few good reasons:

* It's made by Pippin Williamson, a developer I have a lot of respect for.
* The code is beautiful. If you're a developer, I recommend just reading the code to see what code should look like.
* The plugin is easy to extend, which means I have a lot of flexibility to do custom stuff.
* The EDD Members add-on was available, which I only needed to add one feature to.
* I plan to offer digital downloads for purchase other than memberships in the near*ish* future.
* Easily integrates with my own Members plugin.

I thought I'd be building all of this for weeks.  In reality, the bulk of the work was done in one afternoon.  I think that scares me more than anything.  It was almost too easy.

## Issues, comments, etc.

I was able to get rid of a lot of old, *janky* code on the site.  However, I'm still integrating an old system into a new system.  So, there's bound to be an issue or two.  Please don't hesitate to let me know if you find a problem.

If all goes well in the next week or two, I'll do a complete write-up on building a membership site with these tools.