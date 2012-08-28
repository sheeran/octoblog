---
layout: post  
title: "Upgrade to Movable Type 5"  
date: 2010-09-18 12:45  
comments: true  
categories: ['movable type']
---

Just upgraded my Movable Type install to version 5. I only found a few minor hiccups. The only outstanding one is the comment listing on an individual entry page (such as [this one][1].) The MT templates are setup so that if the commenter is me, the top line of the comment box (which is actually a `definition term`, with the comment text being the `definition description`) should be a different color:

    <h4>Comments</h4>
    <dl>
      <mt:If tag="CommentEmail" like="my@email.com">
        <dt class="neal">
      <mt:Else>
        <dt>
      </mt:If>
        <dd>Comment text here</dd>
    </dl>

The MT:IF statement never resolves to true and the `dt` never assumes the `neal` class that assigns the different color. I have changed the Commenter tag to different things (email, name, etc), and it still doesn't work. 

The original error was worse. I'm still using the original template tag format&#8212;`MTIf`, versus the new `mt:If`&#8212; and with that, the whole statement would get skipped and not put the commenter info in a `dt` block at all. I'm not sure why this should matter&#8212; the template tag format changed in MT4 and I never changed any of my templates and everything worked fine. 

_Update_: After messing with this for multiple hours over three days, no matter what I do, I can not get the `dt` element to even generate anymore. The entire 'MT:IF' statement gets skipped. I changed the IF statement multiple times and tested others that worked fine, but I cannot re-create the error where it generates a `dt` element, but doesn't correctly add the class of `neal` to it. Grrrrr. For now I've removed it and all comments will display the same.

[1]: http://www.nealsheeran.com/archives/2009/08/my_hacked_itune.html