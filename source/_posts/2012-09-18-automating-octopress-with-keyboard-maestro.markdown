---
layout: post
title: "Automating Octopress with Keyboard Maestro"
date: 2012-09-18 23:32
comments: true
external-url: 
categories: [octopress, software, blogging]
---

One of things I wanted to with [Octopress][1] is automate as much as possible the process of creating new posts, generating the site and deploying it to my server. Octopress uses Rake tasks for these steps:

	$ rake new_post["Snappy Article Title"]
	$ rake generate
	$ rake deploy
	
Easy enough, but I would rather not have to swap back and forth into the terminal to create and publish a blog post. Using a static-site generator such as Octopress is supposed to be easier, not harder. To me at least.

__Note__: _A word of warning up front. I throw around words here like "shell scripts", "Ruby gemsets" and other nerdy terms, like I know what I'm talking about. I'm swimming in the deep end of the pool when it comes to some of these topics, so take this for what it's worth. My solution works for me, but there could be a much easier way and/or I could be unknowingly sending by bank statements to a sever in Nigeria._

While the Octopress [documentation][docs] is good, Moncef Belyamani has written two excellent tutorials geared towards beginners on [installing Ruby][2] via [RVM][4] and [installing Octopress][3] locally on a Mac. Per his directions, I set up a octopress gemset that is loaded whenever I `cd` into my Octopress directory:

	$ cd code/octopress
	Using /Users/me/.rvm/gems/ruby-1.9.3-p194 with gemset octopress
	
And from there, I issue the various Rake tasks. My first stop at automating this was to use [Keyboard Maestro][6], due to its ability to run shell scripts. Setting a hot key trigger to execute a shell script as simple as:

	#!/bin/bash
	cd Users/me/code/octopress
	rake whatever
	
...did not work. As I dug around, I learned about the differences between interactive shell sessions and ones that aren't. I assumed that my desired Ruby/RVM environment was not being set when this script executes, and my suspicions were confirmed when I found an article about [scripting with RVM][5] on the RVM site. Adding the code snippet from that article fixed my issues. 

### Creating a New Post

My Keyboard Maestro macro for creating a new post is pretty simple. When I hit `Control-Shift-P`, a window pops up and asks for my article title:

<img src="/images/octo-km2.png" alt="keyboard maestro text input" />

The title is captured as a variable and passed to the `rake new_post` command. The full KM macro is here:

<img src="/images/octo-km1.png" alt="keyboard maestro macro" />

Here is a closer inspection of the shell script itself:

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
	rake new_post["$KMVAR_Title"]

The beginning of the script was copied directly from the RVM site and I added the last three commands that change to to my octopress installation, sets the correct gemset and creates the post. To finish the automation, I created a [Hazel][7] rule that looks for any new file in my Octopress `_posts` directory and opens it with [Byword][8]:

<img src="/images/octo-te.png" alt="Hazel rule" />

<img src="/images/octo-byword.png" alt="blank post with metadata in Byword" />

I then add any categories and enter the post content. Save when I'm finished and then two more macros to post the entry. [^1] A possible alternative to this technique would be to skip the `rake new_post` command altogether and use a combination of macros and [Text Expander][9] snippets that creates a file with the correct `year-month-day-title.markdown` format as well as the proper YAML front matter for the post. This technique could be useful in some sort of remote-blogging scenario.

### Generate and Deploy the Site

I use `Control-Shift-G` for another macro to generate the site content, which just calls the exact same script as above, but replacing the last line with `rake generate`. A third macro deploys the site with `Control-Shift-D` and again, the last command is `rake deploy`---which for me uses Rsync to upload my site to my server.

I have all three macros set to "display results briefly"---the normal rake output to the terminal---for positive feedback of the results of the commands.



[^1]: These last two can be combined with the `rake gen_deploy` command, if desired. Other Octopress rake tasks such as `watch` and `preview` could easily be automated with this as well. If the terminal _is_ in your wheelhouse, Alessandro Nadalin has [written][10] some nice shell aliases and functions that combine many of these tasks.

[1]: http://octopress.org/
[docs]: http://octopress.org/docs/
[2]: http://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/
[3]: http://www.moncefbelyamani.com/how-to-install-and-configure-octopress-on-a-mac/
[4]: https://rvm.io/
[5]: https://rvm.io/workflow/scripting/
[6]: http://www.keyboardmaestro.com/main/
[7]: http://www.noodlesoft.com/
[8]: http://www.bywordapp.com
[9]: http://www.smilesoftware.com/textexpander/
[10]: http://odino.org/bash-aliases-for-octopress/