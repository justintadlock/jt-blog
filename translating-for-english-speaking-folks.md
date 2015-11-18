# Translating for English-speaking folks

*Wait? Translating for English-speaking folks? Huh?*

Yes, that's right.  This is a translating tutorial specifically geared toward people who blog in English.  Technically, a non-English user can make use of it too.  The ultimate goal is to teach both audiences the same tricks.

If you didn't know, WordPress is used around the world.  A lot.  There are many different people from all walks of life using it.  We're getting better at making the software much easier for people whose native language is not English to share their ideas and creations with the world.

One of the roadblocks to me has always been the "awareness factor".  What I mean by this is that English-speaking bloggers have it easy.  WordPress is built in their language.  It's easy to be unaware of the extra steps that others have to take to get WordPress and its themes/plugins even up and going.

I often write tutorials from a development perspective because I want to teach other developers how to do something awesome with code.  Today's lesson will be for users because there are already vast numbers of tutorials teaching developers how properly internationalize (prepare for translation) their themes and plugins.

The two goals of this tutorial are to increase the awareness of the global WordPress community for English-speaking bloggers and teach these bloggers the proper way to "translate" things.

## You've been changing text wrong

As a theme author, I often come across questions related to modifying text.  This may be something as simple as a single phrase like "Edit Post" or the footer text at the bottom of the page such as "Copyright &copy; Site Name".

For anyone who has ever translated a theme, this is dead simple.  Just open the <abbr title="Portable Object">PO</abbr> file and *translate* the text.  For most English-speaking users, I either need to teach them how to translate the theme or tell them which file(s) to open and modify.

Modifying files in the theme is not the best option.  Considering all my themes at [Theme Hybrid](http://themehybrid.com) are internationalized, users should be translating any text in their themes they want to change.

I don't blame the users for not knowing how to translate.  It's not something they're aware of.  My hope is that this tutorial will help educate, not just my users, but users of any WordPress theme (or plugin).

## Translating-related things you might want to know

You might hear a couple of words tossed around that are hard to spell and understand.  These two terms are **internationalization** (i18n for short) and **localization** (L10n for short).  For our purposes of translating, these terms are not necessarily important, but it does help to understand them.  I'll try to keep these definitions simple.

* **i18n** is the process of designing software (themes, plugins, WordPress) so that it can be adapted to different languages without having to change the code.  As developers, we do this with built-in function calls that WordPress offers.
* **L10n** is adapting the software for a given language and/or locale. For us, this typically means creating translation files for our themes or plugins.

That's probably an oversimplification of the two terms, but for the purposes of what you need to know, it should suffice.  If you're interested in reading more, here's the Wikipedia article on [i18n and L10n](http://en.wikipedia.org/wiki/Internationalization_and_localization).

## Tools you'll need

There are many different tools for translating.  There's even a few WordPress plugins to do the job.  For me, the best option is [Poedit](http://poedit.com).  It's downloadable software that you use from your computer.  It's got a solid development history, gets the job done, and is simple to use.

I'll be using Poedit throughout this tutorial.  You're welcome to use something else.

## Know your WordPress language

WordPress' default language is U.S. English, which means that your language code is `en_US`.  That's `en` for the English language and `US` for the United States region.

You can change your language by changing this code in your `wp-config.php` file:

	define( 'WP_LANG', 'en_US' );

Technically, you can change the language code to anything.  It can be `justin` or `en_justin`.  It really doesn't matter what you use as long as your translation files use a file name that matches the language.

## Translating theme text

I'm going to focus on themes within this tutorial because this is what I get the most questions on.  However, these same methods apply to both WordPress and plugins as well.

The first thing you need to do is locate your theme's POT file.  This is pretty important because it holds all of your theme's text strings.  For this tutorial, I'll use our latest theme, [Saga](http://themehybrid.com/themes/saga) as an example.  In the theme folder, you'll find a `saga.pot` file located in the theme's `/languages` folder.

Open `saga.pot` with Poedit.  What you'll want to do at this point is go ahead and save this as a new file called `en_US-saga.po`.  Poedit will also automatically create a `en_US.mo` file (this is the machine-readable file that WordPress uses).