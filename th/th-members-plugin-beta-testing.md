# Members plugin beta testing

In 2009, I had just moved back home to Alabama and was living in the spare room at my grandparents' house.  During those few months with nothing but a suitcase and my laptop, I done what I still consider some of my best work and built the first version of the Members plugin.  

It was an eye-opening period where I learned a lot about how things work in WordPress.  I also got a lot of things completely wrong.  There was one point where I even accidentally deleted all capabilities from my Administrator role and locked myself out of my own WordPress install.

For the 6 years that this plugin has been available, I've never given it a major overhaul.  A big part of that was because the plugin simply worked.  It got the job done.  Another part of that is my skills needed to grow to a point where I could actually code some of the things I wanted to do.

This version of members is my attempt at doing those things. 

Some of the new features might seem minor, but that's the point.  I want to keep making the plugin behave as if it were always a part of your WordPress install.

The following are some features that need eyes on them and feedback.

## Multiple roles per user

<img src="http://themehybrid.com/blog/wp-content/uploads/2015/09/multiple-roles.png" alt="Multiple roles per user" width="788" height="311" class="aligncenter size-full wp-image-6522" />

One feature that folks have asked for is the ability to add multiple roles per user.  You can now do this from the edit user screen in the admin (note that you shouldn't be able to change your own role).  All roles are also listed on the users screen in the admin.

One thing to note is that the change role dropdown on the users screen will overwrite all roles.  I toyed with the idea of just disabling this, but I find the feature useful when bulk editing.

## Edit role screen

<a href="http://themehybrid.com/blog/wp-content/uploads/2015/09/edit-role-screen.png"><img src="http://themehybrid.com/blog/wp-content/uploads/2015/09/edit-role-screen.png" alt="Edit Role Screen" width="1183" height="593" class="aligncenter size-full wp-image-6523" /></a>

Perhaps the biggest visual change in the plugin is the UI of the edit role and add new role screens.  It received a major overhaul.

I needed a way to introduce the concept of "denied" capabilities.  In previous versions of the plugin, you could add (grant) or remove a capability from a role, but there was no way to explicitly deny a capability.  When building a complex site with multiple roles per user, the difference between a role being granted a capability, being denied a capability, or simply not having a capability becomes important.

Not every plugin user will need this level of functionality.  However, adding the functionality forced me to completely rethink the UI because the old UI simply would not work.  I believe this change is a good thing all around.

Please note that I haven't fixed some UI stuff for mobile and smaller screens yet.

## Other changes

There's a significant number of other changes as well, such as more developer-oriented features to better create add-on plugins, a new settings screen, and allowing HTML for the content permissions meta box (yes, I know folks have been asking for this).

All of these features need testing too.  And, I'll definitely go into more details about add-on plugins when the plugin update gets released.

## How to beta test

You can grab a copy of the [development version](https://github.com/justintadlock/members/tree/dev) from GitHub.  If you prefer ZIP files, there's a link to download it on the right-hand side of that page.

I cannot stress this enough:  <strong>Only test this plugin on a dev/test install.  If you use it on a live site, you do so at your own risk.</strong>  Seriously, this is a beta version of something that makes direct database changes in WordPress.  It's best to play it safe until it's been fully tested.

Also, please excuse the messy code.  When you're *in the zone*, neatness and inline docs may get thrown out the window.  I'm working on cleaning things up.  I wanted to get the ball rolling on beta testing though.