---
layout: post
title: "A Standard Test Post"
date: 2012-08-26 12:44
comments: true
categories: [octopress, test]
---

This is a sample entry to test [Octopress][1]. It will include [Markdown][2] syntax, as well as some of the unique capabilities of Octopress itself. This entry was written in [Byword][3], and excellent markdown-enabled text editor for the Mac.

Here is some *emphasized text*, and this text is contained in a **strong tag**. While I'm at it, backticks can be used to denote `code blocks`. Markdown will auto-convert apostrophe's, 'single quotes' and "double quotes" to their appropriate HTML entities. An en-dash is two hypens: 1974--1996, and an em-dash is three---before I forget, type all the ampersands you want (&) and ellipses can be created with three periods...

Other static-page generators I looked at, in varying degrees of detail:

1. [Pelican][4]
	1. Written in Python
	2. Not that it really matters.
		1. Sub-sub bullet one
		2. And two
2. [Middleman][5]
3. [Nanoc][6]
4. [Kirby][7]

A quick glance at an unordered list:

- Power, Corruption, and Lies
- Brotherhood
- Technique
- Substance
	- First New Order album I owned
	- Temptation still one of my favorite songs of all time

Let's include an image.

{% img http://www.nealsheeran.com/lab/prototypes/img/lightning.jpg Lightning Over Water %}

Octopress includes many options for including a `code` blocks. First, three backticks make a simple code block:

```
.description {
    float: right;
    text-align: right; 
    }
 ```
  
  Syntax highlighting is included as well.

{% codeblock Thanks to Brett Terpstra lang:ruby %}
  if File.exists? configfile
  $conf = File.open(configfile) {|f| YAML.load(f) }
  if $conf['debug']
    puts "Read config from #{configfile}..."
    $conf.each {|k,v|
      puts k+": "+v.to_s
    }
  end
{% endcodeblock %}

Sweet. Github Gists can be included as well:

{% gist 3046554 %}

More awesome. Here is a basic blockquote:

{% blockquote %}
People sleep peaceably in their beds at night only because rough men stand ready to do violence on their behalf.
{% endblockquote %}

These can include the source:

{% blockquote  Peter Gulliam, Tinker Tailor Soldier Spy%}
In that case, Toby, I'll be sure to be ultra, ultra quiet.
{% endblockquote %}

And you can easily quote Tweets, with links and everything:

{% blockquote @iowahawkblog https://twitter.com/iowahawkblog/status/239832255223177217%}
If we have learned anything from Game of Thrones, it is the frailty of unsustainable whore-based economies.
{% endblockquote %}

 



[1]: http://octopress.org
[2]: http://daringfireball.net/projects/markdown/
[3]: http://bywordapp.com/
[4]: http://pelican.notmyidea.org/en/3.0/index.html
[5]: http://middlemanapp.com/
[6]: http://nanoc.stoneship.org/
[7]: http://getkirby.com/