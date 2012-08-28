---
layout: post  
title: "Syncing Lightroom 3 with Aperture"  
date: 2010-07-10 02:49  
comments: true  
categories: [software, photography]
---

I've [written][1] before about Adobe Photoshop Lightroom versus Apple's Aperture and I currently use Lightroom as my primary photo management and editing tool. However, Aperture still has it's uses: It is much easier to sync picks to my iPhone via Aperture (by selecting the desired albums under the photo tab in iTunes) than manually exporting from Lightroom. Lightroom also has no equivalent to Apple's photo book tool. Previously, I would select my desired picks and export them as TIFs to a folder in my Pictures directory. I would then apply a specific color label to indicate which ones resided in Aperture. This worked fine because I only 'developed' images in Lightroom, but if I ever went back and applied new develop settings or presets, none of those updates would carry over to Aperture. 

<img src="/images/lr1.png" width="435" height="260" alt="Lightroom Publish Service screen capture" />

With the release of Lightroom 3, much has been made of the new Publish Services, although most of this attention has been paid towards publishing images to online services such as [Flickr][2][^1]. Lightroom can also publish images to your hard drive and any changes made to these images can be updated with the push of a button. _And these changes can be easily updated in Aperture._ Here are the steps I use: 
   
1. I created a Lightroom Publish Service set to export TIFs to a specific folder.
2. Drag my desired images to this service and select "Publish."
3. In Aperture I import the images from the specific folder into a  project. Nothing earth-shattering here.
4. If I modify any of these images' settings in Lightroom, they will be identified as needing to be re-published.
5. After re-publishing in Lightroom (which updates the TIF in the desired folder), I return to Aperture and under the Photo menu, I hold down the option key, which changes the Update Preview menu item to Generate Preview:

<img src="/images/ap1.png" width="440" height="437" alt="Aperture Photo menu screen capture" />

This will force Aperture to reload the image, but without having to re-import the image. Now there is a live link between those photos that exist in both Lightroom and Aperture and if I make any further changes in Lightroom, it is easy to see those changes in Aperture. 

When new photos are added to this Publish Service in Lightroom, just go back to Aperture and select Import to add them to the library. I keep all of these Lightroom exports in the same project and two key points if you do as well: ensure the original project is selected as the destination or a new one will be created and check that 'do not import duplicates' is selected. 

I have only tested this with develop settings. I don't know if any metadata changes like updated keywords will be reflected in Aperture. Since I use Lightroom as my primary asset management program, I'm not so concerned if these changes don't make it over. I also haven't looked at how this would work on a large scale. Of the 7000+ pictures in my Lightroom catalog, only my top picks&#8212;less than 200&#8212;are exported to Aperture. Feel free to comment if you notice any problems with this workflow.


[^1]: I find Lightroom's built-in Flickr Publish Service inadequate because it lacks the ability to publish to a specific photoset. I use Jeffrey Friedl's very thorough [version][3] instead.


   [1]: http://www.nealsheeran.com/archives/2008/09/adobe_lightroom.html
   [2]: http://www.flickr.com/photos/sheeran/
   [3]: http://regex.info/blog/lightroom-goodies/flickr/publish
