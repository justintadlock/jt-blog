# Role groups in the Members plugin

<img src="http://themehybrid.com/blog/wp-content/uploads/2015/09/members-role-groups.png" alt="Members Plugin: Role Groups" width="841" height="432" class="aligncenter size-full wp-image-6619" />

As I gear up for the 1.0.0 update of the Members plugin, it's time to start talking about some of the new developer-centric features.  

One of the big things I wanted to do with this release was open up ways for other plugin developers to integrate their plugins.  Members is already a popular plugin among developers in the WordPress community, but there has been little in the way of direct integration.

## The role groups idea

A tweet by John James Jacoby, project lead of BuddyPress and bbPress, made me go ahead flesh out one of the hidden features of this release.

https://twitter.com/JJJ/status/642206718722707456

Just the thought that someone else could really use role groups made me sit back down at the drawing board and build in a method that would allow a plugin like bbPress, for example, to create a "Forum" or simply "bbPress" group really easily.

This was already on my mind, but the existing method required two filters.  I needed to make that easier.  So, the Role Groups API was born.  It'll be bare-bones in this version, but it will allow plugin developers to start integrating with minimal code.

## How to create a role group

Members now has a conveniently-named hook `members_register_role_groups` to hook in and create your custom groups.  You need to use the `members_register_role_group()` function.  

The following is a quick example.

	add_action( 'members_register_role_groups', 'jt_register_role_groups' );
	
	function jt_register_role_groups() {
	
		members_register_role_group(
			'jt_group',
			array(
				'label'       => esc_html__( 'JT Group', 'jt-textdomain' ),
				'label_count' => _n_noop( 'JT Group %s', 'JT Group %s', 'jt-textdomain' ),
				'roles'       => array( 'role_a', 'role_b', 'role_c' ),
			)
		);
	}

Well, that's pretty much it.  *Did I forget to mention how ridiculously simple this is?*

When you register a role group, the group is added to the views list on the Users > Roles screen in the admin.  It will allow users to view and manage the roles specifically in that group.

The `members_register_role_group()` function takes in two parameters: `$name` and `$args`.  The `$args` parameter accepts the following array of arguments:

* **label** - Internationalized text label for the group.
* **label_count** - Internationalized text label when showing the role count.
* **roles** - Array of roles belonging to the group.
* **show_in_view_list** - Whether to show the group in the view list on the roles screen. Defaults to `true`. Out of the box, this is really the only functionality, so you should probably keep this enabled.

## Anything more you can do with groups?

At the moment, there's not much else that can be done with direct integration.  There's a few useful functions within the plugin's `admin/functions-role-groups.php` file that might be of interest.

I think the exciting thing would be if someone built an add-on plugin for Members that allowed users to manage custom role groups.  The API and hooks are there.  So, feel free to go wild if you're interested in that.



























