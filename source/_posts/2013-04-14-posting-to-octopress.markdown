---
layout: post  
title: "Posting to Octopress, Part 2"  
date: 2013-04-14 14:40  
comments: true  
external-url:  
categories: [octopress, blogging]  
---

Shortly after I converted this blog to Octopress, I [came up][1] with some Keyboard Maestro macros to automate the rake tasks to create posts and generate/deploy the site. I have moved away from that workflow for a few reasons:

- I had to come up with a post title right off the bat. Sometimes the title comes to me at the end. Granted, the actual title of the post is driven by the YAML title, but the URL for the post comes from the filename. 
- I didn't like having drafts living in my `_posts` folder. An errant `rake generate` could publish a draft if I wasn't paying attention. Yes, one can put `published: false` in the Yaml front matter, but one more thing I would have to go back and change. I also have a Hazel rule that [archives and tags][2] entries that would trip before I even added a category.
- Creating an 'elsewhere' post involved a lot of copying/pasting: URLs, titles, quotes...you can probably guess where this is going.
- No mechanism to write a post on an iOS device.
- I didn't have a KM macro to push to my git repository. Another extra step.

So rather than wrap some duct tape around my KM macros to address these issues, I started over, with some help from others. My new writing and posting process is based on the following:

1. The Octopress `_posts` directory should be a final, 'canonical' destination. A markdown file only goes there when it is about to be published.
2. Be able to draft a post using any text editor on my Mac. My previous KM macro was tied to Byword.
3. Even though I write the majority of these posts on my Mac, have the ability to draft a post on an iOS device
4. Pave the way to easily *publish* a post from a iOS device.

Tools I use to do this: [Text Expander][te], [Drafts App][drafts], [Dropbox][db], and [Hazel][hazel]

### Local Drafts ###

Some blog posts start in nvALT as a few random snippets and some links. For others, I fire up MultiMarkdown Composer. I usually don't care about the YAML front matter until the very end. Or maybe I dump it in first. If the latter, I need to go back and change the YAML date. Here is the Text Expander snippet for basic YAML front matter (triggered by `.opnp`):

    ---
    layout: post  
    title: "%|"  
    date: %Y-%m-%d %H:%M  
    comments: true  
    external-url:  
    categories: []  
    ---

The same date/time string is in a standalone snippet to just update the date for a draft right before publishing: `.opt --> %Y-%m-%d %H:%M`. I save these files to the desktop with any filename, and an extension of `.txt` or `md`. When it comes to time to publish, another TE snippet is triggered with `.opf`, and the cursor is ready to type the rest of the filename:

    %Y-%m-%d-%|.markdown

Files don't get the `.markdown` extension until they are ready for publishing, for reasons I'll get to shortly.

For an 'elsewhere', or linked-list post, I am indebted to Doug Rice of [Jarhead][3] for the following Text Expander snippet:

    ---
    layout: post
    title: "%snippet:safaricurrentpagetitle%"
    date: %Y-%m-%d %H:%M
    comments: true
    external-url: %snippet:safaricurrentpageurl%
    categories: [elsewhere, %|]
    ---
    
    > %snippet:safaricurrentpageselectedtext%

Text Expander 4 can call snippets from within snippets, and this one will automagically look at the front-most tab in Safari and put the page title and the URL in the front matter, as well as the URL. Any selected text is added as a blockquote. The cursor ends up in the category array, ready to add any additional ones.

While my 'normal post' snippets works on my iPhone, the linked-list version does not, as the three sub-snippets are actually AppleScripts.

### Drafting Posts on iOS ###

Drafts App for iOS is the obvious choice here. I have an action called "OctoPost" that will send the draft post to a folder on DropBox. I have the filename set to the following predefined format:

    [[date|&Y-&m-%d]]-[[title]].md

Drafts can accept strftime strings for the date component of a proper Octopress filename, and can set any desired extension, but there isn't really a way that I can see to set the rest of the file name, which becomes the URL.

The `[[title]]` snippet above takes the first line of the draft, but a normal Octopress post needs the YAML front matter to be first: `---`. As written, this draft will need a title in the first line that would subsequently need to be moved to the appropriate YAML line (or deleted).

### Publishing ###

Hazel rules for the win. The focal point for publishing posts is a 'launch' folder on my Desktop called `OPDRrafts`. Any files from the Drafts App folder get copied to this folder. This desktop drafts folder has two primary rules:

{% img center http://www.nealsheeran.com/images/octo-hazel1.jpg 'Hazel Rule screenshot' %}

This changes the color label of the folder red, as an alert that a new draft is present. The Apple script is needed to make the folder change itself and is as follows:

    tell application "Finder"
       set posix_parent_dir to POSIX path of (container of (item theFile) as text)
    end tell
    return {hazelSwitchFile:posix_parent_dir}

The second rule does all the heavy lifting. When a post is finished, I change the extension to `.markdown` to trigger the rule:

{% img center http://www.nealsheeran.com/images/octo-hazel2.jpg 'Another Hazel Rule screenshot' %}

The rule moves the final markdown file to my `_posts` directory and then executes a shell script:

    #!/bin/bash
    # Load RVM into a shell session *as a function*
    if [[ -s "$HOME/.rvm/scripts/rvm" ]] ; then
    
    # First try to load from a user install
     source "$HOME/.rvm/scripts/rvm"
    
    elif [[ -s "/usr/local/rvm/scripts/rvm" ]] ; then
    
    # Then try to load from a root install
     source "/usr/local/rvm/scripts/rvm"
    
    else
    
     printf "ERROR: An RVM installation was not found.\n"
    
    fi
    cd /Users/me/Code/octopress
    rvm use 1.9.3@octopress
    git add . && git commit -m "New Post" && git push origin 2.1 && rake generate && rake deploy;

The key action is the last line, which comes from [Alessandro Nadalin][4] and conveniently commits the change locally, pushes the changes to my git repo, generates and deploys the site. With a nifty Growl notification telling me so.

### Summary ###

1. Write posts either locally, or with an iOS device, using Text Expander snippets for YAML front matter and to create file names. Local files can be anywhere, and iOS drafts will get put in the 'launch' folder.
2. Once complete, change the extension to `'markdown` and if required, drop the file into the desktop 'launch' folder.
3. About 90 seconds later, the post is published on the site.
4. A second copy of the post is archived and tagged with [Open Meta tags][2].

If you have an always-on Mac such as a Mac mini, you could easy publish a post to your site with nothing but an iPhone or iPad using Dropbox and Hazel rules, but there is the issue of getting Drafts app to name the file correctly. Of course, an iOS editor such as Byword or Writing Kit that connects to Dropbox and allows complete control of filenames fixes this.

[1]: http://www.nealsheeran.com/archives/2012/09/automating-octopress-with-keyboard-maestro/
[2]: http://www.nealsheeran.com/archives/2013/01/openmeta-octopress/
[3]: http://jarhead.me/2012/11/automate-link-posts-textexpander-chrome/
[4]: http://odino.org/bash-aliases-for-octopress/

[drafts]: http://agiletortoise.com/drafts
[db]: https://www.dropbox.com/home
[hazel]: http://www.noodlesoft.com/hazel.php
[te]: http://smilesoftware.com/TextExpander/index.html
