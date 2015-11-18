One of the reasons I originally got involved with the Theme Review Team was to add a little balance to what I and many other theme authors felt like were overly strict guidelines dealing with how themes should be coded.  We needed more voices from experienced people doing this theme thing.

Standardization is almost always a good thing.  However, it is not good when it stands in the way of innovation.  The one thing I've fought long and hard for is to make sure the TRT doesn't stifle innovation in any way if it can be avoided.

I think we've all heard it before &mdash; "If you're not doing it this way, maybe your theme just isn't right for our repository".  That's directly in opposition of the plans for the theme repository, which is to provide the best free WordPress themes in existence.  Sometimes, our way isn't the best way.  I even like to think of myself as a pretty darn good developer, but I'm continually amazed at some of the cool techniques that theme authors are employing in their themes.  Often times, these techniques simply clash with our guidelines.  It's not bad code; it just doesn't fit into our standards.

## The need for standards

Don't get me wrong.  We absolutely need standards and to continue improving on our guidelines.   And, there are things where we need to draw a pretty hard line.  Anyone who knows me, knows that I'm a stickler for standards.

Frankly, we see a lot of bad code coming through the review process.  Without guidelines to guide reviewers and theme authors, it'd be a mess.

However, we must recognize that there are some people out there doing some awesome stuff that's not going to fit into this nice, neat little box we want everyone to fit into.  If we're stopping these themes from making into the repository, we're not doing our jobs.  We're failing as a team.

We need to be able to recognize when theme authors are writing good code that doesn't match up with what we think a theme should be.  Admittedly, I've fallen short in this myself and have been a bit too strict at times.  I hope to do better in the future.

## What prompted this discussion?

In our weekly meeting, it was mentioned that a `comments.php` template (loaded via the `comments_template()` function) should be required in all repository-hosted themes.  It had already been decided that this wasn't a requirement, but it was brought back up for discussion.  It's a rarity that a theme author would do anything different anyway.  However, there are many ways (using core WordPress functionality) to display comments.

This discussion went on to say that the use of `get_header()`, `get_footer()`, and `get_sidebar()` should be required.

Yes, we absolutely should be using those functions **if** our intention is to load those templates.  That's not really in question.  What's in question is whether we should require their use.

Anyone who has been around theming for a while knows that the only theme files required for a properly-working theme are `index.php` and `style.css`.  If we begin requiring the use of specific templates, we're doing a major disservice to the theme development community.  We will make certain that they cannot innovate when it comes to templates.

There's a case to be made that the use of those functions will fire certain hooks that plugins may use.  That's definitely true.  However, that's a slippery-slope to go down.  I can sit here and rattle off any number of hooks that may or may not be fired, depending on which functions or features a theme decides to use.  I'm prepared to go down that slope, but it won't get us anywhere.

## An ongoing issue

This is not a single, one-off issue that we've had.  It's part of a larger issue that has been going on for years.  Standards are good only when they don't get in the way of good developers innovating.

Some of the awesome stuff we have today with theming would never have been possible if those theme authors were building themes within the current era and trying to get their themes on the repository.

If our goal is to make every theme the same, I'm not so sure this is a community I want to be a part of.  If our goal is to have quality themes with good code, we need to be able to think outside of our set of standards once in a while.

We've made great strides in the past few weeks in getting rid of some legacy stuff, clarifying existing guidelines, and making things a little less strict.  I want us to continue down this path.