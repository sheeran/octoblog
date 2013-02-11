---
layout: post  
title: "Project Tasks in Sublime Text 2"  
date: 2013-02-10 19:57
comments: true  
external-url:  
categories: [software, productivity]  
---

This is a productivity nerd post that *is not* about OmniFocus. Not that I dislike OmniFocus, I own and use it, but it is not always the right tool for the job. 

One of my larger projects is redesigning this site. It has been an ongoing affair, and at various times the rather large task list associated with it has moved from OmniFocus, to a Markdown outline in nvALT, with a brief stint as a [taskpaper][tp] document. 

Since 96% of my time with this project involves hammering away in a text editor writing HTML and CSS, all of these suffered from being a bit too far removed from the project itself. In addition, I found the OmniFocus "paradigm" to be a tad constricting--contexts where pointless, and it doesn't lend itself to large chunks of text.

My editor of choice is [Sublime Text 2][2] and there are two excellent plugins available for it that make keeping track of any web, software, or writing project a breeze.

### [Plain Tasks][2]

{% img center http://www.nealsheeran.com/images/plaintasks.png 'Screenshot of a Plain Tasks TODO file' %}

Plain Tasks is like having taskpaper embedded in your Sublime project. It treats files with certain extensions (.todo, .tasks, etc) as special documents with their own formatting and shortcuts. Lines ending in a colon are projects, and tags can added with the `@tag` style. Keyboard shortcuts include '⌘ D' to mark a task complete and 'Shift ⌘ A' to move all completed tasks to the Archive section at the end of the list. Check the plugin [tutorial][3] for the full lowdown.

The main benefit I get out of using this is I have a `lab.TODO` file that lives in the root in my redesign folder and I open it first to see what needs to get accomplished. Invariably when I'm working on one aspect of the site, a related task or idea arises that I need to capture quickly. Rather than switching to completely different app, my task list is just a tab away (⌥ ⌘ left/right arrow to cycle through open tabs). Significant friction reduction, as the productivity dorks say. 


### [Sublime TODO][1]

Plain Task works great for keeping track of things with a wide scope. For fine-grain task-foo, I use Sublime TODO, which can easily keep track of all your tasks, down to the line level. I have a line in a Sass file for the new site that looks like this:

```
//TODO: Convert this font-size to a mixin
.lab-list dt,
.lab-list dt a { 
  font-size: 18px;
}
```

Open Sublime's Command Palette (Shift ⌘ P), then type `todo` and select from either of two options: Search TODOs across all project files, or just open files. The resulting tab looks like this:

{% img center http://www.nealsheeran.com/images/sublimetodo.png 'Screenshot of Sublime TODO results' %}

The plug-in will find every instance of `TODO`, `NOTE`, `FIXME`, and `CHANGED` across all the applicable files. The comment patterns can be customized in your user settings file, or on a per-project basis. The killer aspect of this plugin is you can navigate the list with the `n` or `p` keys and when the desired item is highlighted, press return. The file will open at the specific comment, with the cursor at the beginning of the line. [^1]

{% img center http://www.nealsheeran.com/images/sublimetodo2.png 'Screenshot of going to TODO comment' %}

This tool isn't necessary limited to code or HTML/CSS. You could litter your next angst-ridden hipster novel (written in Markdown, of course) with `FIXME's` and `NOTES`, and this plug will find them all.

The big advantage of having both of these tools basically embedded in the project is also a potential disadvantage: they *only* live with the project. No iPhone access to my web redesign tasks. No awesome iCloud sync.

Me: so what. If an awesome idea for the site explodes forth while buying some kick-ass gas station coffee, I'll just dump it in my OmniFocus inbox and process into my Plain Task list later. 

[^1]: How awesome would it be if OmniFocus could do this? Highlight "Buy Milk", hit return, and be magically transported to the dairy aisle at Safeway. Since version 2 is already in work, I'll give the Omni group until 3.0 to get this done. Or I'm switching to back to Things. They'll knock it out right quick.

[st]: http://www.sublimetext.com/
[tp]: http://www.hogbaysoftware.com/products/taskpaper
[1]: https://github.com/robcowie/SublimeTODO
[2]: https://github.com/aziz/PlainTasks
[3]: https://github.com/aziz/PlainTasks/blob/master/messages/Tutorial.todo
