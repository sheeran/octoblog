---
layout: post  
title: "Upgrading My 2010 MacBook Pro"  
date: 2013-07-17 00:25  
comments: true  
external-url:  
categories: [mac, geekery, software]  
---


I recently hit the three year mark on my current Mac, a Mid-2010 15-inch MacBook Pro. Things were getting a bit sluggish, so it was time for some upgrades.

First off, I doubled the RAM with 2 x 4 GB memory modules from [Other World Computing][owc] for $83, replacing the stock 4 GB the system came with. This difference alone was noticeable.

My stock 500 GB hard drive is only about half-full, but this was as good a time as any to put in an SSD. Also from OWC, I ordered a [240 GB Mercury Electra 3G SSD][ssd] ($220). I elected for the 3G over the faster 6G Extreme model since System Profiler says my MacBook runs at the lower speed anyway [^1], and I saved about $70 in the process. Yes, there are cheaper SSDs out there, but I have never done wrong when buying from OWC, so they got my money.[^2]

I also purchased a [Data Doubler][dd] kit ($38) in order to remove the hardly-used Superdrive and put the old stock 500 GB hard drive in in its place for more storage. Finally, for $35, I got an external [USB enclosure][slim] for the removed Superdrive in case I need it.


### Preparation

First, I re-downloaded Mountain Lion from the Mac App Store (since it disappears after installation). I then used a tool called [Lion Disk Maker][ldm] to easily make a bootable installer on an unused 20GB USB drive I had laying around.

I then made sure the critical software on the computer was up-to-date and made one last clone to my FireWire backup drive using [Super Duper][sd]. I booted from both the installer drive and the backup drive to ensure that they worked. [^3]

The next step was to ensure important apps that can sync files with Dropbox did so: 1Password file, Text Expander snippets, Keyboard Maestro macros (in the new version 6), and manually added some for apps that didn't, such as Hazel. How much you sync really depends on how much of a clean start you want on the new installation. I wanted to begin with a blank slate, so I didn't copy over preferences/data files for every single app.  

If I forgot anything, I would have the old hard drive installed in the optical bay anyway, plus the clone.

I also made a new note in nvALT where I just brain dumped anything related to setting up a new machine: critical apps, apps that are critical but easily forgotten because they run in the background, various settings tucked away in odd places, links to various guides/how-to's, etc.


### Hardware Installation

**1. The SSD**

Very straightforward, I just followed the [video][owc-ssd] on the OWC site. When I was finished, I put the back cover back on, but left the screws out since I would be going back in shortly to install the Data Doubler.

I then booted from the Mountain Lion installer drive and installed the operating system. And behold the huge performance increase of a clean OS install on a brand new SSD. Once I verified that the the install went fine, I shut the machine back down and removed the cover again for the next step.

**2. Install the old hard drive in the optical bay.**

This was the trickiest part, and having the correct tools is important (like magnetic screwdrivers). I used three separate  guides, all of which were specific to my computer model:

- The OWC [install video][owc-dd]
- The hardcopy instructions that came with the drive
- An iFixIt set of [instructions][ifixit]

All the above were very helpful, but they differed slightly in one area. There are two black connector cables that have to be carefully disconnected from the logic board to get the optical drive out. In between these two there is a *tiny* silver connector cable, which I believe is for the camera. The OWC video did not remove this cable, but the other two sources did. I gave it a tug and it didn't move. Not wanting to damage anything, I left it connected and just carefully moved its cable out of the way when I did remove the optical drive.

I then closed everything back up and turned the machine back on. Again, the performance increase is well worth the expense.

**3. Removed Superdrive**

The included instructions made installing this into the separate enclosure quite simple. It took almost as long to find an actual disc to test it. 


### Software Installation

With a 240 GB SSD and a 500 GB HDD in my MacBook Pro, this was as good a time as any to take a hard look at all the crap that has accumulated on my machine over the years and only install the apps and data that I really need. I purposely *did not* restore from my clone or use Apple's Migration Assistant to move anything back over. Yes, this means this process takes longer, but I think it's worth it.

My game plan with this storage setup was to use the SSD for applications, and keep the majority of my data on the old hard drive. Matt Gemmell's blog post *[Using OS X with an SSD plus HDD setup][mg]* had the perfect recipe for this, which is using symlinks to point folders such as `Pictures` and `Music` on the SSD to their equivalents on the hard drive.

The first set of apps I installed were Dropbox and nvALT, for reasons mentioned above, and 1Password, since I keep all my software licenses in it.

I then fired up the Mac App Store to install the next set of apps, and encountered a slight hiccup. I went to the Purchases tab and the vast majority of apps that I needed indicated *Installed*, when they obviously weren't. Well, actually they were. The MAS app saw the apps on the old hard drive now sitting in the optical bay.[^4] 

Since I was going to do a format and erase of the old drive anyway before I moved any big hunks of data onto it, this was not a major issue. I wiped the drive and the MAS app showed all apps available for installation, and I had the FireWire clone available to copy my data back onto the hard drive. 

I then copied all my data over, with working files going to the SSD and big folders such as `Pictures`, `Movies`, and `Music`, using the folder setup in Matt's [article][mg].

**Tip:** One of the first things I did on the new machine is start a new note in nvALT that serves as an "install log"; a running list of apps installed, issues encountered, etc. I have a section that lists all the random Terminal commands that I use to enable/disable certain features of OS X. Here is one that enables copying text from a Quick Look window [^5]:

    defaults write com.apple.finder QLEnableTextSelection -bool TRUE; killall Finder
    
Lastly, in order to get this blog post up, I had to recreate my development environment on the command line. Since this site is powered by Octopress, which needs Ruby and Git, I followed Moncef Belyamani's *outstanding* (and recently updated) tutorial, *[How to Install Xcode, Homebrew, Git, RVM, Ruby & Rails on Snow Leopard, Lion, and Mountain Lion][ruby]*. I followed his steps to the letter with zero errors. I then copied my blog directory over from my old backup, ran `gem install bundler` and `bundle` and everything was back to normal.


### Backup Plan

A new drive setup means time for a new backup clone. I'm keeping my old clone in a drawer--I never know when I may need something from it. I purchased a new 1 TB Firewire drive and partitioned it to match the sizes of my new SSD and the data hard disk. Now I run SuperDuper to clone each of those to their respective partitions on the new FW drive.

With two drives and their associated backups, I spent a fair amount of time coming up with names for the drives so their relationships to each other would be easy to remember. Dorky, yes, but somewhat necessary. The drives are called *Overlord*, *Bodyguard*, *Ultra*, and *Enigma*. World War II history buffs should get the reference. 

I hope this has been helpful. I'm now off to reboot my machine one more time to marvel at the speed of the SSD.

### Useful Resources

* TidBits, *[SSD Optical Drive Replacement Speeds a Sluggish MacBook Pro][tb]*
* TUAW, *[How do I setup a Mac with both an SSD and a regular hard drive?][tuaw]*
* Matt Gemmell, *[Using OS X with an SSD plus HDD setup][mg]*
* Brett Terpstra, *[The first apps on my new Mac][bt]*

[^1]: Thanks to this [TidBits article][tb] or I wouldn't have checked.

[^2]: The [Samsung 830][sam] is highly regarded and currently $175.

[^3]: With a bootable drive plugged in, hold down `option` after the startup chime to be able to select it.

[^4]: The same thing happened when the FireWire clone was plugged in.

[^5]: For an excellent list of these, see Mathias Bynens' [dotfiles][osx]

[owc]: http://www.macsales.com
[ssd]: http://eshop.macsales.com/item/Other%20World%20Computing/SSDEX3G240/
[sam]: http://www.amazon.com/Samsung-MZ-7TD250BW-Series-Solid-2-5-Inch/dp/B009NHAEXE/ref=sr_1_2?ie=UTF8&qid=1373664859&sr=8-2&keywords=samsung++SSD
[dd]: http://eshop.macsales.com/item/OWC/DDAMBS0GB/
[slim]: http://eshop.macsales.com/item/Other%20World%20Computing/VLSS9TOPTU2/
[tb]: http://tidbits.com/article/13133
[ldm]: http://liondiskmaker.com
[sd]: http://www.shirt-pocket.com/SuperDuper/SuperDuperDescription.html
[owc-ssd]: http://eshop.macsales.com/installvideos/macbookpro_15_unibody_mid10_ssd_m/
[owc-dd]: http://eshop.macsales.com/installvideos/macbookpro_15_unibody_mid10_dd_m/
[ifixit]: http://www.ifixit.com/Guide/Installing+MacBook+Pro+15-Inch+Unibody+Mid+2010+Dual+Hard+Drive/8520/1
[mg]: http://mattgemmell.com/2011/06/21/using-os-x-with-an-ssd-plus-hdd-setup/
[tuaw]: http://www.tuaw.com/2012/01/20/ask-tuaw-how-do-i-setup-a-mac-with-both-an-ssd-and-a-regular-hd/
[bt]: http://brettterpstra.com/2013/03/26/the-first-apps-on-my-new-mac/
[osx]: https://github.com/mathiasbynens/dotfiles/blob/master/.osx
[ruby]: http://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/