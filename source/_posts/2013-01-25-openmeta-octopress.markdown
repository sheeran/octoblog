---
layout: post  
title: "Assign OpenMeta Tags to Octopress Posts"  
date: 2013-01-25 21:07  
comments: true  
external-url:  
categories: [octopress, geekery, software]  
---

In a [previous post][1] about Pinboard, I mentioned how I use OpenMeta tags to tag all kinds of different files on my local machine and then search for them using an app like Tags or Leap. The one missing piece is a script that goes through all of local copies of my Octopress blog posts, reads the categories and assigns them as OpenMeta tags. Not anymore.

For a while I have been using Hazel to copy new posts from my Octopress `source/_posts` directory to an Archive folder in my Dropbox (that also holds my Pinboard archive, my Twitter archive [^1], etc). The script lives in this Archive directory and applies the tags to the copies, not the originals. This script requires the OpenMeta [command line utility][7] to be installed [^2]. Here are the highlights and the full script is [here][2].

{% codeblock cats2tags.rb lang:ruby https://gist.github.com/4584424 Get Gist %}
# Set ARCHIVE to a correct directory (and extension)
 
require 'yaml'
 
archive = "#{ENV['HOME']}/Dropbox/Archive/OctopressPosts/*.markdown"
 
Dir.glob(archive) do |post|
  readin = YAML.load_file(post)
  title = readin['title']
  tags = readin['categories'].join(', ')
  
  %x{/usr/local/bin/openmeta -a #{tags} -p #{post}}
    
  puts "#{title}: #{tags}"
end
{% endcodeblock %}


First off, a big thanks to [Brett Terpstra][3] for helping me out with this script. And this is the very first script I have ever written, so it is very likely there is a better way to do this. There are some additional caveats that I'll get to below. The script does the following:

1. Goes through every Markdown file in my Archive directory and reads the YAML front matter using the Ruby YAML module
2. Creates a variable, `tags` that holds a string of all the post categories, comma-separated.
3. Calls the OpenMeta command line utility to assign these `tags` to each markdown file.
4. The last `puts` line writes the post title and the tags to the terminal, which is useful if you call this script from the command line.


But having to fire up the terminal and run this script every time I make a new post wouldn't very nerd-like, would it?  I have another Hazel rule that looks at the Archive folder and runs the script when a new markdown file appears. 

{% img center /images/om-hazel.jpg 'Hazel screencapture' %}

In order for Hazel to be able to run the script, make it executable with the following command in the terminal:

    chmod a+x /path/to/your/script.rb

### Notes and Caveats:

(*All due to my status as a complete Ruby noob and easily fixed with some more knowledge*)

1. Categories need be formatted as follows in the YAML front matter, with brackets. Even for a single category.

    `categories: [foo, bar]`
    
2. It currently only works with single word categories. I use a few multi-word categories on this site like `categories: [test, 'web design']`, but this script would write three OpenMeta tags: `test`, `web`, and `design`. This is not a problem for me since all the other tags on my machine are single word. Since I have a fair amount of `webdesign`-tagged files from Pinboard, I used BBEdit to find all instances of `'web design'` and replace with `webdesign`. Another reason why I do all of this on copies of posts--I can keep the two-word categories on the website.

3. This script is useful if you have a large collection of posts[^3], but not very efficient when run with the Hazel rule as new posts are archived, as it will unnecessarily process every file again (although it won't duplicate tags). My next step would be a modified version that just writes tags against new files. 


### So Why Do This?

Tagging files make finding stuff much easier than drilling down into folders. I have over 1500 OpenMeta-tagged files in various places on my hard drive. Most are in DropBox, but many specifically are not, and I use a variety of tools to find them.

I really like the Finder replacement, [PathFinder][4]. You can tag files from the app and OpenMeta tags can be displayed in any list view. Here is a screenshot of my Octopress archive folder:

{% img center http://www.nealsheeran.com/images/om-pf.png 'Pathfinder screencapture' %}

I also use[ Leap][5] to search for tagged files across my computer. Here is a screenshot of my 'octopress' tag, showing archived Pinboard links, blog posts, nvALT notes, and a Jekyll  screencast:

{% img center http://www.nealsheeran.com/images/om-leap.jpg 'Leap screencapture' %}


Leap also has a nifty tray that slides out from the side of the screen when you drag any file. Drop the file on it and a tag window with a list of recently used tags appears:

{% img center http://www.nealsheeran.com/images/om-leap2.png 'Leap Tag window screencapture' %}


[Tags.app][6] is my go-to tagging mechanism. `Shift-Command-Space` brings up a window similar to Leap whenever a file is selected. Both apps are smart and use tag completion in their windows. Tags also has a search shortcut, which replaces the Spotlight search window:

{% img center http://www.nealsheeran.com/images/om-tags.png 'Tags screencapture' %}

OpenMeta tags are awesome and while their future in OS X is a bit [cloudy][9], they are still a key tool for me for keeping things organized and finding them later.


[^1]: I use Tim Bueno's Python Tweet Archiver [script][8].

[^2]: The OpenMeta CLI documentation is a bit sparse, but from messing around with it, it basically uses this syntax: `openmeta -a tag1, tag2 -p /path/to/file`. The `-a` attribute 'adds' tags. You could use `-s` to replace all existing tags. I'm sure there are other options and tags can be passed a number of ways, but once I got it working, I stopped digging.

[^3]: It took about 90 seconds to write tags to just over 400 posts in my archive.
    
    

[1]: http://www.nealsheeran.com/archives/2013/01/how_i_use_pinboard/
[2]: https://gist.github.com/4584424
[3]: http://brettterpstra.com/
[4]: http://cocoatech.com/pathfinder/
[5]: http://www.ironicsoftware.com/leap/
[6]: http://www.caseapps.com/tags/
[7]: http://code.google.com/p/openmeta/downloads/detail?name=openmeta_commandline_1.3.0.zip&can=2&q=
[8]: http://www.timbueno.com/2012/07/07/rolling-my-own-automatic-tweet-archiver
[9]: http://support.cocoatech.com/discussions/problems/1387-openmeta-standard-and-mountain-lion

