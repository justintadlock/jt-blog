Lance Willet opened an [interesting discussion](http://make.wordpress.org/themes/2013/11/10/guidelines-shouldnt-fail-a-theme/) on the Make Themes blog.  This discussion was prompted by a WordPress [trac ticket](http://core.trac.wordpress.org/ticket/25008 "Twenty Fourteen: Add word-wrap to title, avoid overflows") in which the Twenty Fourteen theme didn't follow a particular theme review guideline.

I've decided to post my response on my own blog for a number of reasons:

* I'd wager more theme authors read this blog, particularly those who don't currently have a theme on WordPress.org.
* Most of the discussions of the WordPress.org theme review team, while technically public, are really not known by the larger part of the WordPress theme author community.
* Theme authors who might be too intimidated to reply there might be open to having their say here in my blog comments.
* My response is probably a bit lengthy for the comments thread there.

I've thought many times about writing a similar post to Lance.  He brings up a lot of valid points about our current theme review process, points that I've seen other, lesser-known people bring up only to be shot down by our rigid attitude toward alternative views.

When I first joined the Theme Review Team, it was because Matt Mullenweg asked me to do so.  I brought up similar points, but he told me (paraphrasing from what I remember) that if I joined, it'd be an opportunity to balance out some of strictness of other reviewers from someone who had actually been building themes for a while.  At the time, there were only a few of us, so it was possible to balance things out back then.  Now, we have a much larger team and a much larger set of **guidelines** (not rules, folks).

I've even brought this up on my own [theme forums](http://themehybrid.com/support), asking my users if they'd mind if I dropped my themes from WordPress.org and ran my own hosting service.  The response was overwhelmingly positive.  They've seen how much work I've put into making sure my themes pass a lot of "guidelines" that I don't believe should be taken as rules and the level of stress this can sometimes cause.  And, this is coming from someone who's been doing this a lot longer than most theme authors. 

This has been an ongoing, internal discussion I've had because of the current review process.  Particularly, over the last year or so, we've become much stricter in our handling of the guidelines.  

Right now, we don't have guidelines.  We have hard-and-fast rules that we call guidelines because that sounds friendlier.

## No iteration

My biggest issue with how we handle theme reviews at the moment is that most theme authors cannot ship 1.0.  The theme review team has taken away the iterative process of software development and made it so that the first version you get into the hands of users is perfect, which I believe goes against everything Matt said about [shipping early and often](http://ma.tt/2010/11/one-point-oh/ "1.0 Is the Loneliest Number").  If WordPress itself had the theme review team's philosophy, we'd never get a new release out the door.

At the moment, I might spend two or three months putting together a theme, a large part of that process dedicated to making sure the theme passes all the theme review requirements.  However, once I finally get the theme on the repo, it's done.  I rarely have anything else to do to make the theme better in the future.

I'd rather get the theme into the hands of users after a month of work and update it as I get feedback from users.  That's something I can do with plugins, which have nowhere near the same level of constraint.  With themes, I'm so tired of looking at the theme by the time it's ready for approval, that I'd rather not ever look at it again.

## Guidelines are not rules

I don't know how many theme reviewers are aware of this.  I know for a fact that some of them don't understand this, which is why I feel the need to point this out in our mailing list discussions at times.

A recent example was a question brought up on the mailing list about whether a theme is allowed to have multiple theme settings screens.  The reviewer was immediately told that all settings are **required** to be on a single screen.  Only documentation and some other items were allowed separate screens.

[My response](http://lists.wordpress.org/pipermail/theme-reviewers/2013-October/016166.html):

> Aside from what others have already said, the "one settings page" guideline should be taken as a guideline and not a 100%, set-in-stone rule.  I have no problem with a theme doing something like what WordPress does with the custom header and custom background screens.  Of course, this should be within reason. Basically, don't just say, "no you can't do that," without giving it some thought and looking into what the theme is actually trying to accomplish.

[Chip Bennett's reply](http://lists.wordpress.org/pipermail/theme-reviewers/2013-October/016167.html):

> We operate under the assumption that *every* Guideline can be made an exception, if valid rationale is presented. The Guidelines are the starting point/assumption, and from that point, rationale can be provided to justify doing something outside those Guidelines.

I completely agree that we *should* operate under that assumption.  However, on the whole, we do not operate this way.  One need only look through the plethora of [Themes Trac](http://themes.trac.wordpress.org) tickets or read through the mailing list replies to see it isn't how we operate.

At times, some theme authors (myself included) have to fight tooth-and-nail just to keep a specific feature in their theme.  For those unwilling to take part in this fight, they either have the option of not hosting their theme on the official repository or removing the "offending" code.

Part of the problem with this is that not all theme reviewers are at the same level.  That's understandable.  Not everyone knows the WordPress code base inside and out.  However, when those theme reviewers come to the list with a question or clarification on a guideline, they're given strict rules to follow in their review.  This rule is then passed down to the theme author.

## A change in attitude

I know this isn't the intention &mdash; it certainly wasn't when I first joined &mdash; but we currently operate under the assumption that all themes are broken until they've been vetted by our approval process.  That seems a little backwards.

We operate on this principle because in the past we had people trying to get spam into the repository.  Spam getting through isn't a problem nowadays though because that's something we can stop fairly easily.

I've talked with many theme authors who have had trouble getting themes approved on the repository.  I've even had theme authors request that I step in on their review because they believed their theme review was not handled appropriately or for some other issue.

## How 'bout those standards you preach?

Many of you are aware of my efforts for theme authors to follow a set of standards.  I stand behind what I've said in the past and will continue learning and educating others in this area.  However, there is a point where standards do conflict with innovation.

As an example, I'll bring up a recent issue I and another theme author had concerning the guideline that themes must use the `body_class()` function in their theme's `<body>` tag like so:

	<body <?php body_class(); ?>>

That's a wonderful guideline, except when it's used as a set-in-stone rule.  The sole reason for this guideline is so that plugin authors can filter the `body_class` hook and add their own classes.  However, filters are not actually called via the `body_class()` function; they're called within `get_body_class()`.  Wouldn't it make sense that a theme should be allowed to use either function?  Or, more important, that the `body_class` hook is used?

What happens when a theme wants to innovate a little and do something different like the following in their header template?

	<body <?php themename_body_attributes(); ?>>

And, this next bit in their functions.php?

	function themename_body_attributes() {

		$out = '';

		$attr['class']     = join( ' ', get_body_class() );
		$attr['itemscope'] = 'itemscope';
		$attr['itemtype']  = 'http://schema.org/WebPage';

		$attr = apply_filters( 'themename_body_attributes', $attr );

		foreach ( $attr as $name => $value )
			$out .= !empty( $value ) ? sprintf( ' %s="%s"', esc_attr( $name ), esc_attr( $value ) ) : esc_attr( " {$name}" );

		echo trim( $out );
	}

That becomes a problem and does not pass the guidelines, even though it is a perfectly-valid bit of code.  Fortunately, this particular case eventually got a pass after [some discussion](http://lists.wordpress.org/pipermail/theme-reviewers/2013-August/thread.html#14515), despite some of the negative replies.

The reasons I bring up this particular example are:

* Guidelines are good if you use them as guidelines and not full-on requirements.  
* Some theme reviewers are open to discussing the guidelines and making changes where need be.  This is something I want to see continue and a lot more of.
* It was this type of innovation and forward-thinking in themes like Sandbox, Thematic, and Hybrid that earned the `body_class()` function a spot in core WordPress.  Yes, it was done in those themes long before WordPress adopted it.

Theme authors sometimes need to break away from those rigid rules to create awesome stuff.

## The market always decides

In our case, the theme user community rather than the market, decides on the quality of themes.  The great thing about free markets is that they tend to correct themselves.  Better products are known as better products because consumers make this decision through use and word of mouth.

We're so afraid to allow a theme with something broken in an edge-case scenario through the door that we're completely controlling the market's ability to correct itself.

Users are going to use the best themes.  Users are going to drop the worst themes.  We also have a user review system on WordPress.org to help with that.  And, believe me, you're a lot more likely to get negative comments than positive ones; people often get vocal when they notice something broken.

If a theme author wants more users and better reviews, he'll listen to what the users have to say.  That's how you build quality products:  on the feedback of users in real-world scenarios.

## Proposal for a better process

Having guidelines is great.  I want us to continue using those and making them more useful for theme authors.  However, a theme should never fail a theme review because of not meeting a guideline.

My proposal is that we have a set of strict rules for items that are absolute blockers.  There are issues like spam, security, and other problems that we cannot allow to get through.  

The guidelines would be separate from the rules.  Any guidelines the theme author meets is just icing on the cake.  Any guidelines the theme author fails to meet will afford us the opportunity to educate the theme author, but it shouldn't be grounds for rejection.

We sort of have a system like this now, but they're all wrapped under the title "guidelines".  I want to have clear separation of the two.

Furthermore, the theme review team should not be the sole decision makers in the process of deciding a rule vs. a guideline.  This should be an ongoing and continually-refined set of rules based on feedback from many people like:

* Theme authors in general.
* Core WordPress developers.
* Reviewers from ThemeForest and other marketplaces.
* The theme review team.

If nothing else, there should be a clearer distinction between what things are blockers vs. things that should be fixed but won't necessarily break a site.

* The theme unit test data is the biggest.  This deals mostly edge cases rather than the vast majority of uses.
* Alternative functions for handling things that core WordPress doesn't necessarily handle (and without having to explain through 50+ emails of why it's a valid use case).
* The difference between making a legitimate design decision that simply won't work for all users vs. trying to fit all themes into some sort of generic mold.

On the admin side of things, I tend to be a little more rigid because that's where the majority of security issues crop up and where the majority of things you shouldn't be doing in themes are done.  On the front end though, I'd like to see a little more freedom for theme authors.

## Join the discussion

I'm a firm believer in the theme review team being a great thing for the WordPress community.  That's part of the reason I've continued to stick with the team over the years.

With that said, I think we should always question what's happening with the process.  At times, the process may need to be overhauled or even rewritten from the ground up.  At the very least, it's something that should be continually discussed in the open.