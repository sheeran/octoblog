---
layout: post  
title: "Site Updates"  
date: 2009-08-23 09:49  
comments: true  
categories: [typography, 'movable type']
---

As I continue to dust off some of the rust around here, I changed the fonts served up by the stylesheet. Previously, the main typeface used was Lucida Grande and Trebuchet for Mac OS X and Windows users, respectively. For a bit of contrast and because I like old-style figures, I used Georgia for entry headlines as well as the dateline. 

A while ago, I got the new Microsoft fonts such as Calibri, Constantia, and Corbel as part of Office 2008. And today I was surfing around and was impressed with a site using a font called Segoe, a new system/branding font introduced with Windows Vista. So now I first serve up Segoe, followed by Corbel for content and I added Constantia for headlines and dates. 

	body {
		font-family: Segoe, Corbel, "Lucida Grande",
		"Trebuchet MS", Verdana, sans-serif;
		}
	
	h2, #content p.date {
		font-family: Constantia, Georgia, serif;
		}

I did not modify any of the CSS rules for text size (which is declared using ems from a overall base font-size of 62.5% to make the math easier. See this <a href="http://www.alistapart.com/articles/howtosizetextincss/">article</a> for more info). I find that Segoe and Corbel are much easier to read and cleaner looking at my default entry text size of 14px. At least on my Mac, Lucida Grande was a bit large and heavy at that size. The sidebar text is a bit small now, but surprisingly readable at 12px. 

With the all the body text updated, Georgia was starting to look somewhat out of place. I hadn't paid much attention to the new Microsoft serif fonts, but when I saw that Constantia had old-style figures, I gave it a shot and I'm impressed with the results.

Those two minor changes are a breath of fresh air, just when I was thinking the site design was getting a bit stale. Speaking of which. another aspect of this blog that is starting to get stale is Movable Type, even after I upgraded to MT 4. I've been messing around with Wordpress and have been impressed. More on that in a later post.

### Other Tidbits

The next design-related tweak I want to make is come up with a new header image. ITC Conduit is the typeface used and it could use a update as well. I've never been quite happy with the letter-spacing either. I'm no Photoshop guru, so we'll see...

MT 4 also added the ability to add tags to entries. I went back and tagged some entries without knowing that I still had some leftover default template code in my individual archive template that displayed them. I tweaked that bit and will go back and tag the other entries soon. I think I will still assign posts to categories, but I probably need to update my categories list.

As mentioned below, when I dusted this thing off, I noticed I had accumulated almost 12,000 spam comments. I installed an MT plug-in called <a href="http://mt-hacks.com/blogjanitor.html">Blog Janitor</a> with mixed results. Blog Janitor is supposed to turn off comments on entries older than the user specifies (I set 180 days). Why this capability is not inherent in MT is beyond me. Other users have reported that this plug-in doesn't appear to work with MT 4. Upon installation I had the same results, until I looked closer and saw that comments were disabled on older posts. However, spam comments are still showing up in those entries. Unfortunately, I don't have any indications to the reader that explicitly state that comments are off. Also, it doesn't appear that the plug-in allows me to turn comments back on. 

If you see anything else screwed up, please leave a comment and let me know. At least I think comments are on for this...