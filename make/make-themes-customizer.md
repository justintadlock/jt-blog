## Proposal: Theme options only in the customizer

The WordPress <a href="https://codex.wordpress.org/Theme_Customization_API">Customizer API</a> was added in WordPress 3.4, over two years ago.  In development time, that seems like ancient history.  Since it's release, there have been vast improvements.  In WP 4.0, we seen a lot of additional form fields possible.  And, with each release WP is only making the customizer better.

In the coming team meeting on Tuesday, I plan to propose that all themes use the Customizer API for their theme options instead of theme options screens.  There's quite a bit of support for this proposal.  However, I like to make sure we hear all sides of the story, and I know this is a fairly sensitive issue.

This is just fair warning.

<h2>Where we're at</h2>

The Theme Review Team held back on forcing all theme authors to utilize the customizer.  It was a huge transition away from custom options screens.  It was an entirely new object-oriented API that threw a lot of theme authors for a loop.

I believe part of our goal was to give theme authors time to naturally switch over to the customizer rather than forcing the switch right away.  We almost always force this switch with new theme-related WP features, but we held back this time and allowed theme authors to also use the Settings API.

Unfortunately, we've been seeing a rise in the use of options frameworks/libraries that:

* Don't utilize the Settings API.
* Don't match the WordPress admin UI.
* Have many code issues.

Of course, we've also seen a rise in theme authors utilizing the Customizer API as well.

<h2>Review queue problems</h2>

As many of you know, we've been trying to solve the slowdown problem in the review queues.  One of the biggest reasons tickets get reopened and reasons tickets are hard to get through are custom options frameworks/libraries.  Most of these frameworks simply don't conform to our standards.

If everyone were using the Customizer API, that would help to some degree.  At the very least, we could recognize the proper methods for adding panels, sections, controls, and settings.

Right now, each reviewer is having to learn a new options framework every time they review one of these themes.  Frankly, that just seems silly considering that WordPress core has had a standard theme options feature baked in for over two years.

The review queue problems are a secondary reason for this proposal.

<h2>Letting go</h2>

I know there's going to be some pushback against this idea.  We've heard it every time the idea has even been mentioned.

Many of the issues I've heard about the customizer before from theme authors have now been solved.  I imagine there are many that will never be solved satisfactorily because it's simply a different system that we all must learn to adjust to.

Here's the great thing:  WordPress is open source.  Anyone can contribute.  Just about anyone who has ever contributed has found something wrong or something that could be done better.  If there's something about the customizer that you want to see changed, open a ticket in Trac, create a patch, and give the open-source process a chance.

With that said, I want to give you all a chance to voice your opinions in case you can't make Tuesday's meeting.


