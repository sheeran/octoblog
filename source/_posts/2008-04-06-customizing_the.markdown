---
layout: post  
title: "Customizing the Movable Type Bookmarklet"  
date: 2008-04-06 21:23  
comments: true  
categories: ['movable type', blogging]
---

The _Elsewhere_ mini-blog howyadoin' over in the sidebar is actually a separate blog in my Movable Type installation. I use the [Multiblog][1] plugin to pull the 15 most recent posts and display them here. A cool feature is Multiblog's ability to set triggers so that when a new _Elsewhere_ post is published, the main blog automatically updates. 

There is one problem with this: when posting with [MarsEdit][2], the trigger doesn't work. The [documentation][3] for Multiblog is not, ahem, the most helpful, but some digging around got me this [tidbit][4] from Multiblog creator David Rayners: 

>MultiBlog does not currently support rebuilding upon posting from an XML-RPC client. 

As I [mentioned][5] a few days ago, I use MarsEdit because I could _easily_ customize what exactly it puts in the Entry Body field. The javascript QuickPost bookmarklet created by Movable Type opened with the Entry Body field already filled in with `<a title="Page Title" href="the.url">Page Title</a>`. What I want is the Entry Body filled in with the URL only. Since MarsEdit won't trigger my MultiBlog rebuilds, I had to go back a find a way to bend the MT bookmarklet to my will. 

Some digging around the Movable Type [forums][6] showed that other people were interested in modifying the bookmarklet to suite their needs, but not the specific answer to my problem. And the info I did glean was based on an older version of MT. Eventually I found out that the file I needed to tweak was the _CMS.pm_ file located in the _/lib/MT/App_ folder of my MT installation. After some searching, I found what _looked_ like what I needed at line 2256: 

	$param{text} = sprintf qq(<a title="%s" 
	href="%s">%s</a>\n\n%s),
    	$bm_link_title,
    	$bm_link_href,
    	$bm_link_title,
    	$bm_text;

Dude, let me say I was about one step away from a duck watching a lap dance in terms of comprehending this. Pearl wizard I am not. Through some trial and error, I changed this snippet of code to the following:

	$param{text} = sprintf qq(%s\n\n),
        $bm_link_href

And it appears to work. Now when I select the MT QuickPost Bookmarklet on a desired page to create an _Elsewhere_ post, only the URL for the page is automatically generated in the Entry Body field. The Title and Extended Entry are blank for me to fill in. Again, the Title becomes the link text and the Extended Entry is my witty description. Now when I post an _Elsewhere_ tidbit, Multiblog kicks in and rebuilds the main index page. My awesomeness astounds. Yes, there are probably about 22 easier ways to solve this entire problem, but this worked.

So now I use MarsEdit (and highly recommend it) for main entries such as this one and I click on the MT QuickPost doohicky for Elsewhere posts.

   [1]: http://apperceptive.com/plugins/multiblog/
   [2]: http://www.red-sweater.com/marsedit/
   [3]: http://www.apperceptive.com/plugins/multiblog/documentation.html
   [4]: http://apperceptive.com/plugins/forums/comments.php?DiscussionID=11&page=1#Item_0
   [5]: http://www.nealsheeran.com/archives/2008/03/tinkering_under.html
   [6]: http://forums.sixapart.com/
