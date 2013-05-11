
---
layout: post  
title: "My Sublime Text 2 Setup"  
date: 2013-05-03 11:22  
comments: true  
external-url:  
categories: [software]  
---


Consider this my obligatory [Sublime Text 2][st2] post. ST2 has become my editor of choice (over BBEdit, among others) based on how powerful it can become through the use of plug-ins. Here a few of mine that I find useful.

### [FileDiffs][filediff]

Package to quickly find the differences between two files with a user-defined keyboard shortcut. Normally, a new tab will open that identifies the changed lines. I have actually turned this off because the awesome aspect of this plug-in is the ability to set up an external diff tool. I use the not-cheap, but excellent [Kaleidoscope][scope]. When I select `Shift-Ctrl-F`, and choose what I want to compare the open file to, Kaleidoscope opens immediately with much better visual indications of what exactly has changed. Very useful. [^1]


### [MarkdownEditing][mde]

Standard Brett Terpstra greatness for writing Markdown in Sublime Text. Auto-pairing of Markdown characters, keyboard shortcuts for pasting Markdown links, and a special color scheme just for Markdown files. Also recommended if you are a [Marked][marked] user is the [Marked Bonus Pack][markedbp], which includes a Sublime Text Build System to quickly preview a Markdown file in Marked. If you are not a Marked user, well... see the next tip, but you should really get yourself checked out.


### [Markdown Preview][mdp]

A very simple package that gives some nice Markdown preview options, in a browser window or a new tab with generated HTML. I use `Option-m` for the former, and it is quite fast.

### [SmartMarkdown][smartmd]

Have your cursor sitting in a Markdown header? The `Tab` key will fold all the text beneath that header. `Shift-Tab` will fold *all* the headers in a document, regardless of where your cursor is. There are also shortcuts for navigating through different headers and increasing/decreasing their level.


### [SCSS][scss]

Write Sass? This gives you syntax highlighting for `.scss` files. Another somewhat-related tip: I use Bryan Jones' excellent app, [CodeKit][codekit] to generate all my Sass files. CodeKit also has its own [Kit][kit] language to create HTML partials. In order to get `.kit` files to have HTML syntax highlighting, go to the `HTML` package in the Package directory and find the `HTML.tmLanguage` file. In the `fileTypes` array near the top, add this line: `<string>kit</string>`. Done.


### [PlainTasks][pt] and [SublimeTODO][todo]

Two excellent plug-ins for managing projects in Sublime Text 2. I wrote about them [here][nbs].


### [Git][git], [SideBarGit][sbgit] and [Git Gutter][gitgutter]

All great plug-ins for integrating git into Sublime Text. I especially like Git Gutter. It adds small symbols in the gutter that indicate added/deleted lines since the last commit.


### [Origami][origami]

Keyboard shortcuts for creating new editor panes and sending documents back and forth between them. The keyboard shortcuts take a bit to become second nature, but definitely worth it.


### [ReadmePlease][readme]

After you have installed all these plug-ins, use this one to quickly get access to any installed plug-in's README file.

### Themes and Color Schemes

I have to yet to find the perfect theme for ST2, but currently I'm running the [Flatland Dark][flatland] theme, along with its color scheme. [Phoenix][phoenix] is another great theme with a lot of options and more often than not I find myself using the dark version of the default Solarized color scheme. 

My current User Preferences file is in a [Gist][gist] here [^2], and if you are new to Sublime, this free [screencast series][tut] at Tuts+ is excellent.


[^1]: I followed the directions to use Kaleidoscope with the plug-in [here][fdwiki], but the app would not open. I believe with Kaleidoscope version 2, the app now places the command line utility `ksdiff` in `/usr/local/bin`. In my FileDiff User Settings file, I had to explicitly set the path to `ksdiff` as follows: `"cmd": ["/usr/local/bin/ksdiff", "$file1", "$file2"]`, rather than creating a symlink to `usr/bin` as described in the wiki.

[^2]: Spaces, not tabs. Two of them.


[st2]: http://www.sublimetext.com

[filediff]: https://github.com/colinta/SublimeFileDiffs
[fdwiki]: https://github.com/colinta/SublimeFileDiffs/wiki
[scope]: http://www.kaleidoscopeapp.com

[mdp]: https://github.com/revolunet/sublimetext-markdown-preview
[mde]: http://brettterpstra.com/2012/05/17/markdown-editing-for-sublime-text-2-humble-beginnings/
[marked]: http://markedapp.com
[markedbp]: http://support.markedapp.com/kb/how-to-tips-and-tricks/marked-bonus-pack-scripts-commands-and-bundles
[smartmd]: https://github.com/demon386/SmartMarkdown

[readme]: https://github.com/roadhump/ReadmePlease
[scss]: https://github.com/kuroir/SCSS.tmbundle
[codekit]: http://incident57.com/codekit/
[kit]: http://incident57.com/codekit/kit.php

[pt]: https://github.com/aziz/PlainTasks
[todo]: https://github.com/robcowie/SublimeTODO
[nbs]: http://www.nealsheeran.com/archives/2013/02/productvity-sublime/

[git]: https://github.com/kemayo/sublime-text-2-git/wiki
[sbgit]: https://github.com/titoBouzout/SideBarGit
[gitgutter]: https://github.com/jisaacks/GitGutter

[origami]: https://github.com/SublimeText/Origami

[flatland]: https://github.com/thinkpixellab/flatland
[phoenix]: https://github.com/netatoo/phoenix-theme

[gist]: https://gist.github.com/sheeran/5506326
[tut]: https://tutsplus.com/course/improve-workflow-in-sublime-text-2/