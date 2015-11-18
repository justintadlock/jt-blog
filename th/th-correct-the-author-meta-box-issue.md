# Correcting the author meta box drop-down

If you've ever created a custom role with a role management plugin such as [Members](http://themehybrid.com/plugins/members), you've probably run into the issue of users with that role not showing up in the post author drop-down.  This is a pretty common occurrence and is a [5-year-old bug](https://core.trac.wordpress.org/ticket/16841) in WordPress that has yet to be fixed.

My recent [Members - Role Levels](http://themehybrid.com/plugins/members-role-levels) plugin fixes the issue by using the deprecated user levels system, which is what WordPress currently relies on.  

My [Avatars Meta Box](http://themehybrid.com/plugins/avatars-meta-box) plugin also corrects this issue in a different way for WordPress 4.4 users.

If you're a plugin developer and creating custom post types that rely on the author drop-down, you're out of luck if your users aren't using one of those two plugins.  However, I have a quick bit of code that I want to share that will fix this for you.

My hope is that we can iterate on this idea and possibly get it pushed into core.

## Why this is now possible to fix

Prior to WordPress 4.4, it was pretty tough to actually work around this particular issue without doing multiple user queries or doing a custom database query yourself rather than using the APIs available through WordPress.

The new `role__in` argument for the `get_users()` function or `WP_User_Query()` class is what's going to make this possible.  This argument is only available in WordPress 4.4 and allows multiple roles to be used in the user query.

Why roles?  We can query all users who have roles with permission to edit the specific post type.

## Getting roles with permission

The first step is writing a custom function to get all roles that have permission to edit, create, or publish posts of a specific post type.

	function th_get_roles_for_post_type( $post_type ) {
		global $wp_roles;

		$roles = array();
		$type  = get_post_type_object( $post_type );

		// Get the post type object caps.
		$caps = array( $type->cap->edit_posts, $type->cap->publish_posts, $type->cap->create_posts );
		$caps = array_unique( $caps );

		// Loop through the available roles.
		foreach ( $wp_roles->roles as $name => $role ) {

			foreach ( $caps as $cap ) {

				// If the role is granted the cap, add it.
				if ( isset( $role['capabilities'][ $cap ] ) && true === $role['capabilities'][ $cap ] ) {
					$roles[] = $name;
					break;
				}
			}
		}

		return $roles;
	}

## Filtering the author drop-down

Now that we can get the correct roles, we can filter the user drop-down and only get users with specific roles.

We also only want to do this for our post type, so make sure to change the two instances of `your_post_type` to the actual name of your post type in the code.

	add_action( 'load-post.php',     'th_load_user_dropdown_filter' );
	add_action( 'load-post-new.php', 'th_load_user_dropdown_filter' );

	function th_load_user_dropdown_filter() {
		$screen = get_current_screen();

		if ( empty( $screen->post_type ) || 'your_post_type' !== $screen->post_type )
			return;

		add_filter( 'wp_dropdown_users_args', 'th_dropdown_users_args' );
	}

	function th_dropdown_users_args( $args, $r ) {
		global $wp_roles, $post;

		// Check that this is the correct drop-down.
		if ( 'post_author_override' === $r['name'] && 'your_post_type' === $post->post_type ) {

			$roles = th_get_roles_for_post_type( $post->post_type );

			// If we have roles, change the args to only get users of those roles.
			if ( $roles ) {
				$args['who']      = '';
				$args['role__in'] = $roles;
			}
		}

		return $args;
	}