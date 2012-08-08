---
layout: post  
title: "A Markdown Test Entry"  
date: 2012-08-07 22:56  
comments: true  
categories: [markdown, test]  
---
Here is a test entry for Octopress. This entry is written in Markdown, using the excellent [Byword](http://bywordapp.com/) app. For more information on using Markdown, check out these links:

* The original [Markdown](http://daringfireball.net/projects/markdown/), by John Gruber
* The more advanced [MultiMarkdown](http://fletcherpenney.net/multimarkdown/) by Fletcher Penney

*Note:* I have set Octopress to use the `kramdown` markdown parser (as opposed to the default `rdiscount`. It expands on the orginal format, specifically implementing footnotes. For more info, check out the [kramdown](http://kramdown.rubyforge.org/syntax.html) site.
 
## Basic Text and Links##

Paragraphs are any blocks of text separated by a blank line. The blank lines themselves can contain spaces or tabs. *Don't* indent normal paragraphs. And that apostrophe in the previous sentence was automagically turned into an HMTL entity. Markdown also takes care of "double quotes" and 'single quotes.' Markdown also does ellipses...which are three periods. 

	Note: \*use backslashes to escape asterisks and use them literally \*

Markdown automatically takes care of ampersands: & and less-than-signs: 4 < 5.

To add a `<br />` tag, end a line with two or more spaces:  
Lorem Ipsum  
Delor   

Text surrounded by single asterisks *is emphasized* and single underscores _work also_. For strong (bold) text, use double asterisks/underscores: **this** and **this as well**. 


### Links ###

Links uses brackets for link text and parentheses for the link itself, [like this](http://www.drudgereport.com/). Reference style links can used as well: [more news][1] and [some more] [2]. Space is allowed between bracket sets in reference-style links.

[1]: http://www.cnn.com
[2]: http://www.foxnews.com "Optional title attribute"

These link references can be anywhere in the document, on a separate line. They can be indented up to three lines. Spaces/tabs allowed after colon and colon attribute can be in double quotes or parentheses.

Can also use implicit reference links that have an empty set of second brackets. For example, [Google] [].

[Google]: http://www.google.com

Automatic links can be created by surrounding URL with angle brackets: <http://wwww.google.com>


## Blockquotes ##

> This is a blockquote.
> And this is a hard-wrapped line.
> So is this one. Markdown wraps these lines in a single `<p>` tag

> New paragraphs in block quotes follow the standard rules, after a blank line.
>>  A nested blockquote, using 2 x angle brackets

## Code Examples ##

Indent text four spaces or one tab to get a code block. Markdown wraps it in both `<pre>` and `<code>`:

	#example {
	  float: left;
	  width: 220px;
	  }

Inline code examples use backticks: a `<span>` tag. The angle brackets are auto-converted.


## Lists ##

Unordered lists can use asterisks, pluses, and hyphens (interchangeably):

+ This is the first item.
+ This is the second item.
+ List items can contain blockquotes, just indent them four spaces:
	>This is a blockquote. It does seem to put `<p>` tags in the third `<li>`, though.
 
We can have list items that also use paragraphs:

+ List items that are separated by a space wrap their contents in paragraph tags

+ HTML source should look like `<li><p>List items that</p></li>`

Ordered lists use 'number - period - space':

1. Here is the first item
2. And we have the second.

Something like this may trigger an ordered list. Backslash escape the period to turn this off:

> *1996\. Then I was commissioned.* 

Horizontal Rules are three asterisks or hyphens, and they may contain spaces:

***


## Images ##

Image tag syntax is similar to links, hence there are two kinds: inline and reference.

	![Alt text](/path/to/img.jpg)

	![Alt text](/path/to/img.jpg "Optional title")

And a reference example:

	![Alt text][id]
	[id]: url/to/image  "Optional title attribute"


## MultiMarkdown Specific Syntax ##

Cross-references: Same format as reference links, but matches a header. Go to the [Links] [] section.

Image (and link) attributes, when using the reference style:

	Here is an ![test_image] [].

	[test_image]: http:///path.to/image "Image Title" width=200px height=50px

Footnotes: MMD allows for footnotes, which I think are awesome.[^note1] They let me write how I think.[^whatever]

[^note1]: With a pinch of snuff for David Foster Wallace.

[^whatever]: Which is all over the place.
	
	Footnotes can have extra paragraphs by having them indented one tab

	* And lists items
	* like this one

MultiMarkdown also does `definition lists`:

Here is the definition term
: And here is the description


Another term
With a synonym
: Hence, another description.
: There can be more than one definition.
