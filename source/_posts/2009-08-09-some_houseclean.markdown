---
layout: post  
title: "Some Housecleaning"  
date: 2009-08-09 22:19  
comments: true  
categories: ['movable type']
---

I just upgraded the site to [Movable Type 4.3][1]. I was fully expecting things to blow up. At first glance, they haven't. We'll know more when I hit Save... 

*Update:* Not a smoking hole yet...The one thing I was worried about is if my old MultiBlog plug-in still worked, so that Elsewhere entries are pulled to the main page. No problems there. This capability is inherent in MT now, but I didn't have to make any changes.

The other area where I had done some tweaking is in the comment section. I used another plug-in, MTIfEqual, do some trickery and color my own comments differently from everyone else's. That plug-in is no longer supported (or I deleted it when I converted), but again, the functionality is now inherent in MT 4. While testing it, I noticed that any comment I posted was "sent to moderation", a feature I had previously turned off. When I went to look for the comments, I couldn't find them in the pending section. I dug around and finally found them in the spam section. Even the comments where I identified myself as me got tagged as spam...*along with the other 12,000 comments identified as such*. Holy smokes, I had no idea that much comment spam was still coming in here. Further investigation showed that the SpamLookup plug-in had my IP address on the blacklist. Additional test comments resulted in this very domain being on the blacklist. I disabled part of the plug-in for now and investigate the anti-spam capabilities a bit later.

[1]: http://www.movabletype.org/2009/07/mt_43_faster_performance_powerful_search_more_page_views.html