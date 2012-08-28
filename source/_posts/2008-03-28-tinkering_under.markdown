---
layout: post  
title: "Tinkering Under the Hood"  
date: 2008-03-28 00:45  
comments: true  
categories: ['movable type']  
---

My Elsewhere sideblog is currently broken. I fixed an error with the RSS feed, but still have to clean the rest of the mess up. I'll get to it tomorrow. Must sleep.

**Update:** Should be fixed now. While poking around, I noticed that the RSS feed for my sideblog wasn't behaving correctly. When using a feedreader, clicking on the title of the post led to a permalink for that post on this site versus the external link that was the subject of the entry. I hadn't even modified that template from its Movable Type default because I don't use it. 

A quick Google search got me [this][1] post, but I couldn't get it to work. I dug a bit deeper and it seems that the way I was creating the posts was the culprit. The Title field contained an `a href` that linked to the external site and displayed my title. The snippet of snarky commentary was contained in the Entry Body field. Although this seemed logical, I think the feedreaders (NetNewsWire, Google Reader, Bloglines) choked on the title (or more specifically, the <link> field) containing an `a href`. 

I changed my input format to putting the plain-text entry title in the Title field, the desired URL in the Entry Body Field, and the commentary in the Entry Extended Field. I then changed the appropriate tags in the RSS template to match. The Movable Type quick post bookmarklet doesn't conform to this, but fortunately the [MarsEdit][2] one can be customized. Mine automatically puts the URL in the Entry Body field, I then fill in the Title and Extended Entry.

Here are the applicable tags from the RSS 2.0 template file:
    
    <title><$MTEntryTitle remove_html="1"$></title>
    <description><$MTEntryMore encode_xml="1"$></description>
    <link><$MTEntryBody encode_xml="1"$></link>
    <guid><$MTEntryBody encode_xml="1"$></guid>
    

And here is the template code for displaying the Sideblog on the site, based on the new setup:
    
    <dl class="sideblog">
    <MTEntries lastn="15">
    <dt><a href="<$MTEntryBody$>"><$MTEntryTitle></a></dt>
    <dd><$MTEntryMore$></dd>
    </MTEntries>
    </dl>
    

Yes, I had to go back and change all my previous Elsewhere entries to match this, but that took less time than figuring out the solution to the problem. A situation that was helped by being lazy the past year and not posting much. I'm sure there was a better/easier way to fix this, but once I got it to work, I quit looking.

[1]: http://blog.movalog.com/a/sideblog-rss/
[2]: http://www.red-sweater.com/marsedit/
