Caveats
-------
The jtools system is a work in progress. It works for me and I've been using it productively for several years now. But do *not* think of it as a system you can just install and start using for yourself. Instead, think of it as a sketch of what's possible. And maybe as a headstart for anyone who wants to make similar tools for themselves.

And just to be clear, let me offer the following apologies and disclaimers in advance:

    1. This is an experiment, not a product
    1. I do not offer tech support of any kind
    1. If one of these tools deletes your manuscript and fills your files with ancient Greek obscenities, I am more likely to laugh than apologize
    1. I'm happy to discuss possible features/extensions
    1. But for now, I'm only likely to implement the ones I want to use myself


Problem
-------
Many authors have discovered Markdown as an efficient text-based markup system for writing prose, and that is a good thing. But while Markdown is a step in the right direction, upon closer examination it turns out to be not particularly well suited to some kinds of fiction. Novels and short stories rarely contain tables, bulleted lists, multiple levels of titles, hyperlinks, etc., so all of the Markdown tags reserved for encoding such textual features go largely unused. Moreover, there are a number of things that _do_ happen reasonably often in fiction for which Markdown does not have efficient encodings. Consider long passages (multiple paragraphs) of text set into italics, indented blocks of text for excerpted materials, or centered paragraphs for included poetry, to name a few I have needed to accommodate myself. 

Then there are the needs associated with the long, complex process of drafting and developing a novel-length work. Wouldn't it be awesome to be able to encode hyperlinks directly in the text of a scene that link out to background information behind the character you've just introduced, or explaining the corporate history of the Big Evil Corp.™ that enters the drama on page seven? Or what about flagging invented words so that you can provide definitions directly where you invented it, and then refer to it later, all without mucking up the text that gets produced when you convert your file to PDF for beta readers?

Against such a mounting pile of special cases, I set out to write a new kind of text-based markup scheme for use by fiction authors. Something that embraces Markdown where appropriate, and that walks its own path where the two diverge. I call it Jeffdown, because my name isn't Mark. :-)

The primary differences are fairly simple. Jeffdown still follows the conventions of using _underscores_ to mark italics and *asterisks* for bold. But where it really shines is in its hijacking of the [square bracket] indicators. Instead of marking hyperlinks, the Jeffdown system uses square brackets to denote comments. Notes to self. Most tools in the Jeffdown system completely ignore any content wrapped in comment markers. The PDF generator produces a comment-free draft you can send to your beta readers. The word-count tool ignores the lengthy notes-to-self so you still get an accurate count of how big the manscript itself is.

But that's just the start. In addition to supporting free-form comments within the quotes, Jeffdown also lets you encode special comments. For example, an invented word like flisky [word 1 The state of being drunk and amorous. Part 'floozy', part 'frisky.'] can be marked up as shown. That way, the jglossary tool can create an instant glossary of all your invented terms, and it's guaranteed to catch only the words you actually used. No need to maintain a separate glossary document that ends up littered with words you invented for draft 1 but that are no longer used in draft 5.

Or maybe you've refered to a place like Eyzam Alahut [location 2 Literally translates as Bones of the Whale, a terrifying spired feature in the middle of the desert where magic literally crackles out of the earth, creating transient monsters and imagery that melt into nothing an instant later. Most of the time.] and want to make a note about what you intended the place to be. 

The point is that these notes can be used to capture almost any kind of useful meta notes, right at the time and place you were typing when the idea came to you. No need to jump to external documents. Just pop a [ and keep going. Very efficient and very flexible.

One last use for the Jeffdown notes is to encode meta data about the file itself. If the first word after the [ ends with a :, Jeffdown takes this as a file data note. I use them to encode things like which pov the scene is told from, and where the scene is set, but the most useful tag by far (to me) has been the order: tag. By putting a time code after that tag, the Jeffdown tools will know what narrative or chronological order to display the scene files in. So the jtoc tool can create extremely handy outlines of your book. Not by regurgitating the plan you had BEFORE you wrote it, but by assembling the active notes included right inside the manuscript files. And if you're like me, you are MUCH more likely to keep those notes up to date than you are an outline specified in a different file, maybe even in a completely different folder.

At its heart, Jeffdown is more than just a system for typing your novel. It's like having an assistant right at your elbow, keeping track of things for you while you write. Or, to put it a different way, Jeffdown isn't a typing tool - it's a world-building tool.

Commands
--------
    1. jtoc - Jeffdown Table of Contents: assembles the list of scenes, in author-specified order, from metadata in the scene files themselves.
    1. jcount - Maintains a wordcount log for the entire length of your project. A new entry gets made every time you commit the files to git or bazaar, or every time you check the word count.
    1. jglossary - pulls together an up-to-the-minute glossary of terms declared in all local scene files, and can also pull in terms from related documents, such as earlier books in a series. Also produces lists of characters and settings mentioned in the text.

Roadmap
-------
vim-plugin-jdown: This will handle wiki-link jumping between scene files and background notes within the manuscript folders, as well as syntax highlighting for .jd files. Historically, I've used a combination of vimwiki and markdown plugins that come close, but the time has come for jdown to have its own dedicated plugins. Unfortunately, my vimscript fu is very weak, so this will take some time. 

jdconvert: The workhorse script that can produce EPUBs, PDF interior pages, beta-reader drafts, and short-story submission manuscripts directly from the .jd files, guided by the jtoc listing. The current version works just fine for me, in the relatively cozy context of my own computer environment, but it's nowhere near usable as an out-of-the-box tool for others to start using.


Dependencies
------------
    So far, only one package has proven itself so useful that I've embraced it throughout the Jeffdown tool ecosystem.

    docopt: For organizing and parsing command-line arguments and displaying help.
