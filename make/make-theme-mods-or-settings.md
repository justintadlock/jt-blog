# Customizer: Theme Mods API or Settings API?

A few days ago, Chip Bennett wrote a good tutorial on the APIs related to theme options and broke down how those APIs can/should be used depending on the context.  If anyone can really go in depth with theme options, it's Chip.  I'm hoping we see more from him on theme options in the future.  I highly encourage <a href="https://make.wordpress.org/themes/2014/11/24/understanding-the-apis-related-to-theme-options/">reading his post</a> to make sure you have the foundation you need.

In this post, I want to cover a question that has been popping up, particularly about the Theme Mods vs. Settings and which to use.

Essentially, we allow three different methods of saving theme options on the repository (technically, there are other methods, but we allow three):

* Customizer API + Theme Mods
* Customizer API + Settings API
* Theme options page created with the Settings API

The customizer is so much easier to use and requires a lot less code.  It's something I strongly recommend.  It's also what I'll be focusing on as I write more about theme options.  This post is going to focus on the first two methods using the customizer.

<h2>Customizer + Theme Mods</h2>

The thing many theme authors get hung up on is that theme mods are saved on a per-theme basis.  So, this means when you switch child themes, any theme mod options will need to be saved again for the new child theme.  Sometimes, users might even see this as "losing their settings".

This is both a blessing and a curse.  I love it because it allows my users to have seasonal or holiday child themes.  Imagine you wanted to have a child theme specifically for the Christmas season with its own color scheme.  It's nice to be able to change those color options just for the Christmas child theme.

What happens when you switch back to your regular theme in January?  Well, it still has all of its unique options saved for it.  There's no work involved except for switching child themes.

The other nice thing is that core WP has hooks already built in for each new theme mod you create.  That's very nice for child theme authors who want to quickly filter options in the parent theme.

<h2>Customizer + Settings API</h2>

I'm less of a fan of the Settings API because it means that an option is saved based on the parent theme.  The great thing about it is that users only have to save options once and not save them again if they switch child themes (technically, you can get around that if anyone wants me to explain the code).

Going back to the Christmas theme example:  What happens when you switch to a Christmas child theme?  In this scenario, you'd have to change your colors.  Then, you'd have to change them again when switching back to your non-holiday child theme.

However, not all theme options need to be changed when a user switches child themes.  Some options make more sense to stay the same, regardless of child theme.

<h2>What about a combination?</h2>

Actually, you can use a combination of both the Theme Mods API and Settings API with the customizer.  It's not an either/or thing.  That's just another example of its awesomeness.  I even encourage this practice in some situations.

I imagine things like colors and fonts would generally make more sense as theme mods.  But, an option to either show excerpts or content on the front page might be better served via the Settings API.

Each option should really be given this consideration rather than blindly doing one or the other.