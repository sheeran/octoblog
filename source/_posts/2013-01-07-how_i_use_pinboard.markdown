---
layout: post  
title: "How I Use Pinboard"  
date: 2013-01-07 22:33  
comments: true  
external-url:
categories:   [software, pinboard]
---

I've long been a fan of the web bookmarking service, [Pinboard][1]. It has gotten a bit of attention lately ([Macdrifter][2] is a fan), so I thought I would quickly document how I use it.

I get links into Pinboard a few different ways. In a browser on my laptop, I use [Delibar][3], a menubar utility that syncs with the service, can be used to search it and sends links with a keyboard shortcut. Sending info to Pinboard is almost a show-stopper for me in other reading apps, but [Reeder][4] (Mac and iOS) and Instapaper both make the cut. Tweetbot is an exception, sort of. It can send links to either Instapaper or Pinboard, but you can't have both configured at the same time. [^1] Stuff I find via Twitter then goes to Instapaper first, and possibly filed away to Pinboard later.[^2]

I also use Brett Terpstra's [awesome script][5] to archive local copies of Pinboard links into a Dropbox folder, with the Pinboard tags applied as OpenMeta tags so they are searchable with Spotlight. I also use an app called [Leap][6] that is great for managing all the tagged files on my computer, including these archived Pinboard links. So now I can do a local search for a tag such as *ruby* or *python* and Leap will find all the files with those tags: pdfs, Pinboard bookmarks, [nvALT][7] notes, etc.[^3] My next project is to write a Ruby script that goes through my local archive of these blog posts (which are just markdown files) and applies the categories of each post to the file as OpenMeta tags. Ok, the project before *that* is to learn Ruby, but whatever.

*Update (30 Jan 13)*: Script written. Here's the [Gist][16] and here is the [writeup][17] on it.

More Pinboard goodness:

- [Pinbook][8] is my app of choice for browsing my links on iOS.
- [Delish][9] is a new OS X app that syncs with Pinboard. Its money feature is the ability to build smart bundles, which greatly expands on Pinboards native [tag bundles][11].
- Sean Korzdorfer has some [good info][10] about using Pinboard.

Bottom Line: Pinboard is my favorite web service, by far. Best $3.92 I ever spent.

[^1]: I used to use an IFTTT [recipe][12] to send Favorited tweets to Pinboard, but Pinboard (for me) is for links only.

[^2]: I use the old ReadLater app to manage my Instapaper account on the desktop, and it does Send to Pinboard. However, this app has morphed into [Pocket][13], which I don't use. I like paying for software. I don't believe the Pocket app includes native Pinboard export.

[^3]: Previously, I used the [Tags app][14], per Terpstra's instructions, as the script tagging engine, as well as tagging local files and to browse all my tags. However, a recent re-install of Tags resulted in the app no longer working with his script, so I used the '[openmeta'][15] command line utility instead. I still use Tags app to tag files, but Leap is now my desktop tag browser of choice.


[1]: http://pinboard.in
[2]: http://www.macdrifter.com/2012/12/yet-more-pinboard-tips-again.html
[3]: http://www.delibarapp.com/
[4]: http://reederapp.com/
[5]: http://brettterpstra.com/2011/04/02/mirror-your-pinboard-bookmarks-with-openmeta-tags/
[6]: http://www.ironicsoftware.com/leap/
[7]: http://brettterpstra.com/projects/nvalt/
[8]: http://www.macstories.net/reviews/pinbook-a-fast-pinboard-client-for-iphone/
[9]: http://macdrifter.com/2013/01/delish-pinboard-app-for-mac.html
[10]: http://www.seankorzdorfer.com/open_notebook/pinboard%20workflow%20and%20notes.html
[11]: http://blog.pinboard.in/2012/08/every_day_i_m_bundlin/
[12]: https://ifttt.com/recipes/search?q=pinboard
[13]: http://getpocket.com/
[14]: http://www.caseapps.com/tags/
[15]: http://code.google.com/p/openmeta/
[16]: https://gist.github.com/4680168
[17]: http://www.nealsheeran.com/archives/2013/01/openmeta-octopress/




