# Designing the box

A few years ago, I wrote an article on [parent/child theme development](http://justintadlock.com/archives/2010/08/16/frameworks-parent-child-and-grandchild-themes) on my personal blog.  At the time, there were plenty of people both agreeing and disagreeing with me.  Of course, few people had been doing parent/child theme development as long as I had either.

The article had focused on the difference between frameworks, parent themes, and child themes.  However, it never explained my vision for how all of these things come together, particularly how parent and child themes should work (we'll leave frameworks out of this discussion).

A few days ago, I sent out emails to people who were interested in creating a child theme for my [newest parent theme](http://themehybrid.com/weblog/revolution-in-theme-design).  The response was overwhelmingly positive.  However, I was then in a position in which I had to explain the vision in technical terms to many people who were unfamiliar with my process.  I'm not sure how well I explained it; thus, I'm behind the keyboard tapping out the words of this article.

## The box

When I refer to designing the box, I'm referring to have a limited set of design options available to the designer.  The design options might include things like colors, fonts, and images.  

Imagine I handed you the most beautifully-crafted wooden box that you've ever seen in your life.  Then, I told you that you are allowed to paint this box.  You can't build new drawers on the box.  You can't add wheels to roll it on the ground.  You can't alter the size or shape of the box.  You're simply allowed to paint the box with any design you want.  The purpose of this is not to limit you as a box painter.  The purpose is to give you the freedom to make the box as beautiful as it can possibly be.

The thing to keep in mind is that you're not the box carpenter.  You're the box painter.  

If you can differentiate between the two, you're well on your way to understanding my vision for parent/child themes because that's it in a nutshell.

## Why have limits on child themes?

The major reasons for limits are the reasons listed in the post I linked to above.  I'm not going to regurgitate that entire post.  I recommend reading it if you're unfamiliar with my philosophy on the subject.

I consider child themes useful for two reasons:

* Upgradibility:  They allow you to make upgrades to the parent theme without losing customizations.
* Skinnability:  You can add custom "skins" to an already-existing theme. This particularly applies to publicly-released child themes.

So, if I created a really nice box, you can do things like make a Christmas design for the box.  A St. Patrick's Day design.  Or, even have spring, summer, autumn, and winter designs.  The box will always look and work like the same box.  It might just have a different paint job.

## The parent themes of the future

The newest theme I'm working on has taken me nearly three months to complete.  I've learned a lot about theme development in that time.  It has also been a culmination of much of the work I've done over the past five or so years.

This theme is just the first theme.

I feel like I'm starting Theme Hybrid anew.  This is going to be a drastic change in direction for this site.  So, I'm going to let you all on a little bit of the plan.

Keeping with the box analogy, my new theme is the first box in a new line of boxes.  This box has an extremely specific purpose.  It's probably not going to be useful outside of that purpose.  That's fine.  However, the good news is that I plan on building other kinds of boxes.  If this first box doesn't suit your needs, there's no need to worry.  There's also no need to try your hand at carpentry.  Let me handle that.  I'll craft a box that's better suited to you.  Then, I'll let you paint it.

## Why is all of this important?

Theme development has gotten much more complex over the years.  Adding custom functionality to a child theme makes it harder for parent theme developers like myself to upgrade the parent theme without worrying about breaking something you've built.

This is why I've given child theme authors a very specific and limited set of guidelines.  These guidelines allow the use of forward-compatible, future-proof code that shouldn't be an issue for a very long time (although, you can never be 100% sure of that).

Exactly 50 people signed up to make child themes for this newest theme.  My hope is that those that make a child theme are a shining example of this vision (assuming they follow all of my guidelines).

With limited options for child theme designers, it allows me to continue improving the theme.  It also allows me to continue perfecting things like handling various screen sizes, non-English languages, right-to-left text, and many other things.

As I build my own child themes for this theme in the coming months, I hope the vision will become clearer.  I'm sure I'll write more on the subject as well.  

In the meantime, who's looking forward to the new theme?  Expect a public release within a week.