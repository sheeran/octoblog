---
layout: post  
title: "Leaving Movable Type"  
date: 2012-08-29 19:51  
comments: true  
categories: ['movable type', octopress, blogging]  
---

This site has been built with [Movable Type][mt] since its inception in the fall of 2002. I started off around version 2.5 and then stuck with them through the licensing fiasco of version 3, the wholesale loss of the blogging engine wars to [Wordpress][wp], and the pretty much abandonment of the software by Six Apart.

Movable Type is still a capable platform, but I think it's time for a change. My biggest complaints---in no particular order---are as follows:

_TL;DR - very soon this site will be powered by [Octopress][octopress]_.

1. The upgrade to MT5 a while back broke some functionality of the site. I have been told that this is fixed in 5.1 (I'm still running 5.03), but the MT upgrade process is not my idea of a good time. While much improved over the years, upgrading my MT install falls close to going to the dentist on my fun list.

2. I'm a huge fun of using Markdown, especially the more capable variants such as [MultiMarkdown][mmd] that include footnotes. I struggled for about an hour to get MultiMarkdown to work with MT and failed. 

3. This site is actually two separate blogs within my MT installation. One blog for the main entries such as this one, and another for the "elsewhere" sideblog. I use the MultiBlog plugin to include the last 15 Elsewhere posts on the main page. The good thing about this plugin was any time a new Elsewhere post was created, the front page would automatically regenerate. The bad thing was this regeneration wouldn't happen if the Elsewhere entry was posted with [MarsEdit][marsedit], my tool of choice for writing entries since almost the beginning. I had to resort to the web interface. I don't like the web interface. I wouldn't like it even if it didn't stubbornly include two pointless `<br />` elements after the URL when I used the quick entry interface. But it does.

4. One thing about this site that I haven't liked is the search results. This could be my fault with the whole two-blogs-at-once thing going on, but the MT search and search results templates are a pain to mess with.

5. Which leads to another issue: the MT [documentation][mtdocs] is not the most helpful and has been poor for a while. Multiple pages are out of date or are confusing to use. To upgrade an MT install requires bouncing back and forth between multiple different pages and sets of steps. [^1]

6. Finally, I think it is safe to say that Movable Type is a dead platform. In the early days, everyone used MT. The only significant tech blogger that I'm aware of that still does is [John Gruber][df]. Six Apart farmed out the software to their Japanese subsidiary long before they sold themselves [outright][mt5]. No one develops for the platform anymore: Movable Type-focused blogs have gone dormant, and the plug-in community is a ghost town.

A group of MT developers were working on an open-source version of the software called Melody that was supposedly going to take the platform back to its blogging roots. I wrote about this [almost two years ago][mt5] (when the program was a year behind), and one of Melody developers even left a comment about their prospects. Now? The Melody project has disappeared into the ether. 

## Requirements

So what do I need a replacement publishing system to do? Here is my list, in rough order of importance:

1. Easily import my existing content. Currently, I have about 125 main articles and 250 elsewhere linked-list style posts. Not a lot by any means. but I made the mistake of not porting over about two years of content when I upgraded to MT3. While my Movable Type blog separates my main and elsewhere entries, I'm not tied to keeping that paradigm, and I'm leaning towards a single stream of posts.

2. I still like MarsEdit, but the text editor landscape for the Mac has changed drastically over the years. I would ideally like to write my entries in Markdown using the text editor of my choice. [^2]

3. Ability to completely dictate the underlying HTML structure of all the different sections of the site: Home page, individual entries, archives, etc. I have a significant re-design in the works and I would like to tailor it to a structure that I find useful, not one forced upon me by a CMS.

4. An easy method to categorize or tag entries, and then be able to find tagged articles quickly. [^3]

5. Easily customize the URLs of posts and other content. I made some poor choices in the early days with MT, so I would like a sensible URL structure that is easy to read and at the same time, easy to redirect or rewrite my previous MT URLs to their new equivalents. I will admit that the prospect of diving into `.htaccess` files is somewhat daunting.

6. A publishing workflow with the least amount of friction, from creating and drafting a post, publishing it to my web server, and editing afterwards, if required. The same goes for modifying the underlying templates and CSS files.

7. Along those lines, I would like to have a complete local version of the site on my personal machine that I can tinker with, and then upload any changes to the live version. I could have done this with MT (and have in the past, but just for testing big upgrades), but didn't.

An ability to post from anywhere, including my iPhone or iPad would be a nice-to-have. This would probably mean some integration with Dropbox, which I use. However, I write better at home, sitting at my machine. I don't like typing on my iOS devices anyway, so this is not a huge deal.


## Alternatives

I have been looking at alternates, in varying degrees of detail, for a while now. They fall into two broad categories: full-fledged Content Management Systems (CMS) and static-site generators.

### CMS Replacements

#### [Wordpress][wp]

The clear winner of the "blogging wars" that kicked Movable Type to the street. I've had WP installed locally under [MAMP][mamp] for a few years and its web interface is excellent, but my biggest issue with WP is its underlying PHP-based template structure. Books have been written (and I read more than a few of them) about how to customize your WP install, and anything but the most simple of changes involves some hairy snippet of [PHP code][wploop]. I have more than a few strikes against Movable Type, but I never had to learn a line of Perl to make it do what I wanted, like having separate sideblog on my site. This was going to be a significant emotional event with Wordpress. I tried about six different "sideblog plugins" for WP, but none of them replicated what I had already.

Combine that the usual gripes against Wordpress such as security issues, the near-requirement for some cache plugin and the high noise level about all things SEO (_read snake oil_) in the Wordpress community all left me looking elsewhere. [^4]

#### [Expression Engine][ee]

Another popular PHP-based CMS, but one that uses a template tag system very close to Movable Type's---a point in its favor. I think Expression Engine is overkill for my simple blogging needs, but the most significant detractor was the fact the EE has no inherent ability to import my existing Movable Type content. This would require a _paid_ [plugin][co] that didn't give me the best feeling it would do exactly what I needed. The ability to tag entries? Another $49 plugin. I'm certainly not opposed to paying for software---I paid for an Expression Engine license---but the path forward with EE looked long, both in terms of time required and my credit card bill.

### Static Site Generators

A not insignificant number of bloggers, at least among those nerdier ones I read, have made the transition to static site generators: programs that take a folder of plain text files (usually markdown) and then generate a full site of HTML files. No database, no security holes, no complicated cache plugins, and just about all install locally and with different deployment options.

I'll cut to the chase and say that [Octopress][octopress] is the best tool of the handful I looked at and it will be running this site very soon. 

Out of the box, Octopress has everything I need. It generates a very capable, responsive site that adapts to any viewport. It includes plugins for including Twitter and Pinboard data (among others), both of which I wanted to add anyway. The command line interface has multiple commands for creating, previewing, generating and publishing entries.  Octopress is written in Ruby, which I know next-to-nothing about, but the [documentation][octodocs] is excellent and the installation took about an hour, start to finish.

The developer of Octopress, Brandon Mathis, has always been responsive to my newbie questions on twitter ([@octopress][octotwitter]). For the those with the less-than-stellar nerd cred, I also recommend two excellent tutorials by Moncef Belyamani:

- [How to Install Xcode, Homebrew, Git, RVM and Ruby on a Mac][tut1]
- [How to Install and Configure Octopress on a Mac][tut2]

My original plan was to move over to Octopress coincidentally with a new redesign, but getting my MT entries imported over took less time than I thought. While the layout templates for Octopress are extensible and flexible, there is still a lot of work to do on that front, and the sooner I can leave the aging behemoth of Movable Type for the lean, plain-text goodness of Octopress, the better.

#### Upcoming Entries Releated to the Move to Octopress:

1. [How to Export from Movable Type to Octopress][1]
2. [Linked List Posts: From Movable Type to Octopress][2]
3. Automating Octopress with Keyboard Maestro
4. Runners Up in the Static Site Generator Contest


[^1]: This same complaint---in spades---could be applied to the Wordpress docs as well.

[^2]: Right now, that is either [BBEdit][bbedit] or [Sublime Text 2][sublime]. For straight up writing, [Byword][byword] is pretty nice too.

[^3]: Why do some blog engines insist on providing date-based archives, usually listed by month? MT and Wordpress have done it since day one (as have I). How is this useful for a reader, especially a new one? When I'm scanning your archive page, am I supposed to guess that July 2009 was a good month for you and take a look? I have never understood this, except for the cynical belief that maybe these monthly lists exist to indicate how long you have been at it in the blogging trenches.

[^4]: I was very intrigued with Macdrifter's [article][macdrifter] about posting to Wordpress with Dropbox, but alas...he has left Wordpress for the static pastures of [Pelican][pelican]. 
 

[mt]: http://www.movabletype.org
[mtdocs]: http://www.movabletype.org/documentation/
[mt5]: http://www.nealsheeran.com/archives/2010/09/time_for_a_chan.html
[wp]: http://wordpress.org/
[df]: http://www.daringfireball.net
[mmd]: http://fletcherpenney.net/multimarkdown/
[bbedit]: http://www.barebones.com/products/bbedit/
[marsedit]: http://www.red-sweater.com/marsedit/
[wploop]: http://www.netmagazine.com/tutorials/master-wordpress-loop
[mamp]: http://www.mamp.info/en/index.html
[sublime]: http://www.sublimetext.com/2
[byword]: http://bywordapp.com/

[ee]: http://expressionengine.com/
[co]: http://brandnewbox.co.uk/products/details/datagrab/

[octopress]: http://octopress.org/
[octotwitter]: http://twitter.com/octopress
[octodocs]: http://octopress.org/docs/
[tut1]: http://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/
[tut2]: http://www.moncefbelyamani.com/how-to-install-and-configure-octopress-on-a-mac/

[gridwriter]: http://gridwriter.com/2012/06/18/brand-new-engine/
[macdrifter]: http://www.macdrifter.com/2012/06/update-to-my-simple-dropbox-blogging-system/
[pelican]: http://pelican.notmyidea.org/en/latest/

[1]: http://www.nealsheeran.com/archives/2012/08/how-to-export-from-movable-type-to-octopress/
[2]: http://www.nealsheeran.com/archives/2012/09/linked-list-posts-mt-to-octopress/