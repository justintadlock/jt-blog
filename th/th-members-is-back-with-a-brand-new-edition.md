# Members is back with a brand-new edition

I'm pretty excited about today. Two months and some 200+ code commits ago, I decided to take on the biggest update to the [Members plugin](http://themehybrid.com/plugins/members) to date.  After busting through several roadblocks and getting some constructive criticism from community members during the process, I believe Members can truly claim the title of *the best user, role, and capability management plugin for WordPress*.

There were two major categories of things I wanted to tackle in this update:

* A sorely-needed UI/UX overhaul.
* Make some oft-requested features available.

While there are still some features I couldn't get around to in this release, many of the code changes will allow me to take them on in future releases.

If you want to skip all the details, go ahead and [grab a copy](http://wordpress.org/plugins/members) or install/update from your WordPress plugins screen.

## New role management screen

<img src="http://themehybrid.com/blog/wp-content/uploads/2015/09/members-manage-roles.png" alt="Members: Manage Roles Screen" width="1173" height="610" class="aligncenter size-full wp-image-6630" />

This version makes use of WordPress' list table class to handle the output of the role management screen.  It won't look extremely different from the previous screen, but it does offer some benefits such as:

* Pagination if you have many roles.
* Screen options tab to show/hide columns.
* Role groups (can be filtered by plugin devs).
* Columns that can be customized by plugin devs.

## New edit role screen

<img src="http://themehybrid.com/blog/wp-content/uploads/2015/09/members-edit-role.png" alt="Members: Edit Role Screen" width="1176" height="610" class="aligncenter size-full wp-image-6631" />

The edit/new role screen received the biggest visual update.  I wanted to give it a similar treatment to the edit post screen in WordPress so that it seemed more familiar and flowed with the rest of the UI.  The following are some of the changes.

* Tabbed groups to quickly find capabilities.
* JS-based interface for several features.
* Ability to grant, deny (new feature), or remove a capability from a role.
* Plugin developers can add custom meta boxes.

## Multiple roles per user

<img src="http://themehybrid.com/blog/wp-content/uploads/2015/09/members-user-roles.png" alt="Members: Multiple User Roles" width="801" height="414" class="aligncenter size-full wp-image-6632" />

Multiple roles per user is a feature that has often been requested over the years. It was my hope that core WP would make this a bit easier, but the ticket for this has gone nowhere in core.  I had to jump through a couple of hoops to make it happen, but I think it's well worth it.

This feature coupled with granted/denied capabilities can make for some pretty powerful stuff.

## Other notable user features

The above is just the major user-facing features.  These were huge tasks to take on.  The "denied" capabilities feature alone meant I had to rethink the entire edit/new role interface to even make it work.

Here's a few other things worth noting:

* The **content permissions meta box** got a facelift. You can now move it to any meta box holder on the screen without it looking wonky. The meta box also now accepts custom HTML.
* **Help tabs** everywhere. While we had help tabs before, I completely overhauled them. So, be sure to click the "Help" tab on Members screens when needed.
* New **settings page**.  Like other things, this received an overhaul as well.  I think you'll like the changes.

## Developer features

In the coming days, I plan to write tutorials on new developer features.  I want you all to start integrating your plugins with Members.

* Role groups.
* Capability groups.
* Edit/New role meta boxes.
* Custom role translations.

I've already written one tutorial on [creating role groups](http://themehybrid.com/weblog/role-groups-in-the-members-plugin).  That's something you'll want to check out if your plugin has custom roles.

Also, if you're interested in working with Underscore JS templating, I encourage you to dig into the code.  The "Edit Capabilities" tab sections and fields on the edit/new role screen are all handled by Underscore templates.

Anyway, have fun with this release!