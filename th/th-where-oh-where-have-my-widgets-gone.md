# Where, oh where have my widgets gone?

<img src="http://themehybrid.com/blog/wp-content/uploads/2014/06/categories-widget.png" alt="categories-widget" width="800" height="436" class="aligncenter size-full wp-image-2418" />

It's been a long time since I coded the first widgets for the Hybrid Core framework.  It was way back in 2008.  I had recently moved home from overseas and was just getting Theme Hybrid off the ground.  Those were the days.  I was on my computer for up to 16 hours a day and sleeping on my sister's couch in Atlanta, just barely covering my $400/month rent + utilities.

The widgets I coded back then have held a special place in my heart because they represent what Theme Hybrid has always been about &mdash; pushing the boundaries of what WordPress can do.  I felt like I was coming into my own as a developer.

Times change though.  Other Hybrid Core theme developers and I are getting the feeling that this awesome feature doesn't matter as much to users as it once did.  After some discussion, we decided that the best course of action was to remove the widgets from the framework.

<em>Wait.  Don't get in a panic if you love the widgets.  There's good news.</em>

<h2>Widgets Reloaded Plugin</h2>

I've nearly always felt that the widgets were best served as a plugin, which is why I eventually released them as a separate, standalone plugin called <a href="http://themehybrid.com/plugins/widgets-reloaded">Widgets Reloaded</a>.  This plugin has been available for years now and works along with any WordPress theme.

<h3>What does this mean to me as a user?</h3>

At the moment, not much.  However, as new themes are released and old themes are updated, the advanced widgets will be taken away.  You'll be using the default WordPress widgets.  When that time comes, you'll have the option of installing the Widgets Reloaded plugin if you wish to continue using the advanced widgets.

<h3>What does this mean to me as a developer?</h3>

If you were using the widgets in your themes, you'll need to inform your own users to install the plugin if they want the widgets.  If you're doing client work, you can simply install the plugin for your client.

It also means the following line of code will be useless, so you can remove it when you update to version 2.0.0 of Hybrid Core:

<pre><code>add_theme_support( 'hybrid-core-widgets' );</code></pre>

<h2>Why was this decision made?</h2>

Like I said, the widgets have held a special place in my heart as part of the Hybrid Core framework and themes built from it.  They're not something I'm letting go easily.  But, here's a list of some reasons that they are being removed.

<ul>
<li>It pollutes translation files with extra strings if a theme isn't using this feature.</li>
<li>Translators have to re-translate these strings with every new theme rather than just doing it once for the plugin.</li>
<li>I'm maintaining the code base in two different places (plugin and framework), which makes it easier to create new bugs.</li>
<li>The average WordPress user has changed over the years and most likely will not understand all of the widget settings.</li>
<li>I have much more development freedom in the plugin because plugins aren't limited by the WordPress.org theme review guidelines, which can sometimes make it harder to try new things (particularly in a case like this).</li>
<li>I hope to one day see widgets handled more like nav menus (under the hood), which would clearly put widgets into plugin territory if that day ever comes.</li>
</ul>

I hope that helps explain things for those of you who were questioning this decision.