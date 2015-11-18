# How do we solve the theme options problem?

Users love options, right?  That's the reason we add them as theme authors.  While I think there's a lot to be said about themes with no options that make sounds design decisions, I won't get too much into that right now.  Rather, this post is about solving the major issue we've had for years as theme reviewers and theme authors trying to get their themes on the repository.

Up until a week ago, we allowed theme authors to create theme options in one of three ways &mdash; Theme Customizer, Settings API, or with custom options pages using the Theme Mods API.  We've since narrowed that down to only allowing use of the Theme Customizer (strongly recommended) and Settings API.  This was a pretty great move, but it doesn't really solve 99% of the issues with theme options.  Most everyone has already been using those things.

Realistically, the problem has come down to education.  There are resources out there available for using these things.  However, those tutorials are often written by programmers who aren't great teachers or writers who are not so good at programming.

One of the things I've always hoped the TRT would become is more of an educational team.  I firmly believe that if we didn't have to spend so much time dealing with theme options, we could spend more time on educating in other areas of the dev/design.

I'm writing this post to open a dialogue for everyone on how best to approach this problem.

## Issues

The issues I'm laying out here are based on my own personal observations and some things that I've heard from other reviewers.  As an admin, I'm tasked with doing final reviews on themes before they go live.  These issues are often missed by the first reviewers.  This is not to lay blame on them.  Frankly, it's a tough job reviewing theme options, especially when no two theme options pages are even coded remotely the same.

### Sanitizing, validating, escaping

By far, this is the number one set of problems we run into.  What I'm seeing:

<ul>
<li>Themes don't do any of these things.</li>
<li>Themes do one thing but not the other (e.g., sanitizing input but not escaping output).</li>
<li>Themes use the wrong functions (e.g., <code>esc_attr()</code> to escape a URL).</li>
</ul>

### Options saved by default

This has become less of a problem recently, but I still see it on occasion.  Themes should be <a href="https://make.wordpress.org/themes/2014/07/09/using-sane-defaults-in-themes/">using sane defaults</a> rather than saving default options to the database.

### Frameworks, libraries, etc.

There are a number of theme options libraries available for theme authors.  These are some awesome tools.  However, what's happening is that theme authors are using these things as a crutch and not learning how the core WordPress APIs actually work.

This creates a problem because it can be hard to explain how to correct an issue if a theme author doesn't have the basic foundation that they need to work with theme options.  This effectively eliminates a great moment to educate theme authors because we're not on the same page.

## Fixing the issues

I'm writing this post because I believe this to be the biggest hangup with themes today.  It's the hardest part of the review process.  It's also one of the most critical because theme options means potential security issues.

I'd honestly love it if all themes would just use the customizer.  That'd solve a ton of problems.  However, it would be too limiting to theme authors who are doing some awesome stuff.  I wouldn't want to punish good devs by requiring the use of the customizer just so we can fix everyone else's problems.

My initial proposal is that we build educational tools/tutorials for handling theme options.  These need to be written more clearly than developer resources because many theme authors don't come from a development background.

Another thing we should be doing is strongly pushing theme authors to utilize the theme customizer.

What are your thoughts?  What do you think will benefit both theme reviewers and authors?  How can we better educate people on these common issues?





