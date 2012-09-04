---
layout: post
title: "How to Export from Movable Type to Octopress"
date: 2012-08-30 20:29
comments: true
external-url: 
categories: ['movable type', octopress]
---

The obviously critical part of converting this site over to Octopress was importing my existing Movable Type Posts. There is a Jekyll [script][script] that is supposed to do this, but I have not used it. Poking around the net, I saw a [post][ee] about someone using an archive template to export Expression Engine posts *into* Movable Type.

Well, MT has archive templates and I thought I could certainly do the reverse and export my entries *out* of MT into markdown files with the correct YAML metadata.

Here is the Archive Template I built---I called it OctoExport:

	---
	layout: post  
	title: "<$mt:EntryTitle$>"  
	date: <$mt:EntryDate format="%Y-%m-%d %H:%M"$>  
	comments: true  
	categories: <$mt:EntryCategory$>  
	---

	<$mt:EntryBody convert_breaks="0" $>​
	
Pretty self-explanatory, but a few notes are in order to make this work correctly. First, I set the `format` attribute of the `mt:EntryDate` tag to match what Octopress is expecting in that field. The `convert_breaks="0"` attribute is important. It tells MT to perform no conversion on the entry text, i.e. export it in the markdown format that I wrote it in. Without it, the Entry Body will be exported converted to HTML. 

Also, If you have any MT entries that are split between `EntryBody` and `EntryIfExtended` (with the accompanying "*Continue reading...*" link), include that tag as well. I have never used that, so I left it out.

The other key part of this is setting the Archive Mapping of this template to export with the correct filename structure that Octopress is looking for:

	2012-08-07-a-markdown-test-entry.markdown
	
After creating the template, go back to the Template Options and create a new Entry mapping[^1]. Select Custom from the drop down menu and enter this:

	%y-%m-%d-%F.markdown 

The year-month-day is obvious, although the values are case-sensitive. The `%F` is a place-holder for the original filename, and using an uppercase 'F' means to drop the original extension (.html) so I can add my own (.markdown). This placeholder also replaces spaces between words with underscores. Use `%-F` (note the hyphen) to use hyphens. Read the [MT documentation][mt] for all possible file path options. I used the former because my original MT entries are published with the following URL structure:

	http://www.nealsheeran.com/archives/2012/07/some_post.html
	
And I want Octopress URLs to do be as close as possible to minimize .htaccess pain later on. If I could go back in time, I would have used hyphens and a slug length longer than 30 characters.

Once complete, I hit 'Publish' and in less than a minute I had 121 markdown files of all my MT entries [^2]. Using my [PGP][pgp] post from last month as an example, here is the name of the markdown file that this archive template created:

	2012-07-12-pgp.markdown
	
And here is it's contents:

	---
	layout: post  
	title: "PGP"  
	date: 2012-07-12 00:18  
	comments: true  
	categories: Software  
	---

	I came across [this article][1] about Phil Zimmerman...

## Some Notes Regarding Categories:

1. If you have assigned multiple categories to a post, MT will list them separated by commas after `categories:`, whereas Octopress needs them to be also enclosed in brackets.

2. Octopress needs multi-word categories to be enclosed in single or double quotes.

For example, if Movable Type exports this:

	categories: Current Events, Software
	
Octopress needs this:

	categories: ['Current Events', Software]
	
Some grep-foo with [BBEdit][bbedit] can easily take care of these issues. Of course, I say that like I knew what I was doing. Not quite.

I still went through each file and double-check image paths, links or any posts that were written in HTML as opposed to markdown. MT's basic markdown parser doesn't understand more advanced syntax (such as [Multi-Markdown][mmd]) that provides footnotes. When I wrote a post with footnotes--usually with [nvALT][nvalt] and previewed with [Marked][marked]--I changed Marked to display the generated HTML and then pasted *that* into [MarsEdit][mars].

I haven't been very diligent about setting the right categories (or tags) in the past, so I went back through the resulting files before I generated them with Octopress.

## Redirecting Old MT Posts

Under Movable Type, individual entry URLs were structured like so:

	http://www.nealsheeran.com/archives/2012/07/some_post.html
	
Using the above export template to export the original slug as the title, and modifying the the `permalink` setting in my Octopress `config.yml` file to:

	permalink: /archives/:year/:month/:title/
	
Will result in Octopress posts living at:

	http://www.nealsheeran.com/archives/2012/07/some_post/
	
I made the following entry to my root `.htaccess` file to redirect the old MT URLs to the new location:

	RewriteBase /
	RewriteRule ^(archives/[0-9]{4}/[0-9]{2})/(.*)\.html$ /$1/$2/ [R]
	
I'm no regex nerd, but the key part here is capturing the _file_ name of the original URL (the `some_post`, with `(.*)`) _without the the html_ extension and passing that as a variable (`$2`) for the the final destination _folder_ of the new URL. Yes, I'm sure there are better ways to write the regex, but it works for me, and makes sense when I go back and look at it later. 

[^1]: If you are testing this and not nuking your MT install just prior to converting to something else. Do *NOT* select the checkbox next to `Entry` in the list of mappings. If you do, this template will become the default for all our entries and when a user goes to view an original, MT-generated entry, it will display the markdown file that is created, not the final, HTML version.

[^2]: The markdown files will be created in the Archive Path you have set under Settings. I could not figure out a way to set the mapping path to write to an arbitrary folder (such as 'export'), even within that Archive directory.

[mt]: http://www.movabletype.org/documentation/appendices/archive-file-path-specifiers.html
[pgp]: http://www.nealsheeran.com/archives/2012/07/pgp.html
[script]: https://github.com/mojombo/jekyll/wiki/Blog-Migrations
[ee]: https://supergeekery.com/geekblog/comments/quick_tip_expression_engine_movable_type_export
[nvalt]: http://brettterpstra.com/project/nvalt/
[marked]: http://markedapp.com/
[mars]: http://www.red-sweater.com/marsedit/
[mmd]: http://fletcherpenney.net/multimarkdown/
[bbedit]: http://www.barebones.com/products/bbedit/