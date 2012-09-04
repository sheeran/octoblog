---
layout: post
title: "Linked List Posts: From Movable Type to Octopress"
date: 2012-09-04 00:18
comments: true
external-url: 
categories: ['movable type', octopress]
---

In the [previous][1] post, I documented how I exported my main entries from Movable Type into Octopress. Here is how I did the same thing for my "linked list" style posts.

In order to use linked list-style posts with Octopress, you need to use the 2.1 branch of the software. Instructions are [here][octodocs1] and further documentation is [here][octodocs2]. The instructions are a few months old and say to use the "linklog-test" branch. I asked the developer, the always helpful Brandon Mathis, and he recommended using the "2.1" branch. I did so and had no issues, other than fixing a few merge conflicts.

My "elsewhere" sideblog was a separate blog installed within Movable Type. The `MultiBlog` plugin was used to pull the latest 15 linked-list style posts and list them in the sidebar of my main page. In what-should-be-standard linked-list style, the entry title link went directly to the external site. There was a separate archive of all "elsewhere" links, but there was actually no mechanism on the site to link to an individual "elsewhere" post.

To export my "elsewhere" posts, I created an Archive template much like the one used for my main entries:

	---
	layout: post  
	title: "<$mt:EntryTitle$>"  
	date: <$mt:EntryDate format="%Y-%m-%d %H:%M"$>  
	comments: true  
	categories: <$mt:EntryCategory$>
	external-url: <$MTEntryBody encode_ampersands="1"$>  
	---

	<$MTEntryMore encode_ampersands="1" convert_breaks="0" $>
	
I stored the external URL in the main body of an MT post and my snarky commentary in the Extended Entry section. Again, the `convert_breaks="0"` line is important so that my original text was exported and not the generated HTML. I wasn't very diligent about cleaning up ampersands in URLs when I wrote those posts, so I had this archive template do it for me.

Additionally, when I wrote these entries, I did not categorize them. Since these entries now exist in the same "stream" as my other entries under Octopress, it was quite easy to do a simple multi-file search and replace across all 250 markdown files in BBEdit:
	
	Find: 'categories:'
	Replace: 'categories: [elsewhere]'
	
I then went back through the entries and added additional categories to the some of the posts. After copying these files into my octopress `_posts` directory, I did get a cryptic error after attempting to generate the site:

	/Users/me/.rvm/rubies/ruby-1.9.3-p194/lib/ruby/1.9.1/
	psych.rb:203:in `parse': (<unknown>): did not find expected 
	key while parsing a block mapping at line 2 column 1 
	(Psych::SyntaxError)
	
That specific ruby file is a parser for Yaml and since it neglected to tell me which file was the offender, I started looking at the second line of the markdown files and figured out that Jekyll, the underlying engine of Octopress, does not like double quotes within the already-quoted `title` value:

	title: "Quote of the Day: "Something Hilarious""
	
Another swing back through the markdown files to change any instances of interior double quotes to single quotes, or remove them altogether.

And I'm pretty impressed with the result. Octopress automagically sets the entry title link to point to the external URL, makes the font-size of linked-list posts smaller and includes a symbol (which is configurable) to further indicate it is a linked list post.

A final note: it takes approximately 45 seconds to regenerate my entire Octopress site, with 373 entries. That's about half the time it took Movable Type to do it.

[octodocs1]: https://gist.github.com/1812265
[octodocs2]: http://octopress.org/docs/blogging/linklog/

[1]: http://www.nealsheeran.com/archives/2012/08/how-to-export-from-movable-type-to-octopress/