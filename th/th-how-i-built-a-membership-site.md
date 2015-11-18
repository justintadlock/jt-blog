# How I built a membership site

A couple of weeks ago, I [launched a major update](http://themehybrid.com/weblog/new-membership-plugins-powering-theme-hybrid) to this site's membership system.  As I promised in that post, I would write a full tutorial on setting up a membership site with the tools that I use.

## Choosing the right membership solution

Choosing the right membership plugin is like choosing the right home.  You have to shop around and really take a look at what's out there to get something that fits your needs.  It has to be within your budget and be something that you're comfortable living with for a long time.

If there's one thing I've learned over the years of people using my own [Members](http://themehybrid.com/plugins/members) plugin, it's that no two membership sites are the same.  It's one of the major reasons I've kept Members to a minimum of features.  It allows me and others to build on top of a solid base.  

For others, you might want a complete solution all packaged together.  I'm not a fan of a single plugin trying to be all things to all people.  Those types of plugins typically end up having many mediocre features rather than one or two great features.

If you're looking for a complete solution, this post might not be for you.  Or, it might be just what you're looking for.  Depending on your site, any one of the options mentioned below might be all that you need.

## The foundation

[Members](http://themehybrid.com/plugins/members) is the foundation of nearly any site I put together.  If I need roles and capabilities beyond what's offered in a stock WordPress install, it's the first plugin I activate.

There's a reason it's one of the most-loved plugins by developers -- it provides and easy-to-use UI for setting up permissions.  From that point, you can build any features you need on top of it.

For my site, I have several custom roles.  For the purposes of membership (there are others), there are four options:

* Subscriber (default WP role)
* Standard Member
* Developer Member
* Agency Member

Each role corresponds to a specific type of membership on the site.

I chose the core WordPress role system for this because it's easy for me to add custom capabilities for each type of membership straight from the Members plugin's role editor.  

The other reason is that I can assign multiple roles to specific users.  For example, I also have a "Theme Author" role on this site.  So, a user could be both a "Developer Member" an "Theme Author".  This doesn't matter too much in terms of running a membership site, but maybe it helps explain a bit about why I chose this route.

## Putting three plugins together

With the foundation laid, I needed a few things to actually make the membership system work:

* A way to get paid, of course.
* 
