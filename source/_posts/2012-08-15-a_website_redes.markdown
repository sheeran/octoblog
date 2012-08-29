---
layout: post  
title: "A Website Redesign"  
date: 2012-08-15 07:11  
comments: true  
categories: ['web design', typography, sass] 
---

I designed this blog as it currently stands, in all of its fixed-width glory, back in 2008. Since then, as I have gotten a bit smarter, I have been slowing toying with updating some of the specific design elements. None of these are very revolutionary, and some are actually old hat for many, but time available is short in these parts. And what time was available was usually spent on the "getting smarter" part. 

The key things that I want to accomplish are as follows:

1. Better typography with typefaces from [Typekit][typekit] and a solid [vertical][24ways] [rhythm][ala].
2. Since grids have become all the rage, get into some of that action.
3. A better color scheme.
4. Implement footnotes, or better yet, "sidenotes" in the margin , much like [Jon Tan][tan] and [Kilian Muster][km].
5. Make my home page more of a "hub" by including data from my [Twitter][twitter], Flickr, and [Pinboard][pin] accounts.


Some of the intermediate steps have been captured in the [Lab][lab] section of the site. Specifically, the [Prototype][proto] section is a living (and somewhat documented) work-in-progress of my efforts so far.

Many design professionals extoll the virtues of Photoshop to create comps and then translate those to HTML and CSS. I built some initial comps for type, colors and initial layout, but being that my Photoshop skills are infantile, I found the process long and laborious. I then changed to building an entire site of boilerplates: [Home Page][home], [Single Article Page][single], [Archives List][arch]. I concentrated on building a proper HTML structure, using new HTML5 elements such as `section`, `article` and `footer`, before adding general and then specific style declarations.
 
Before I get into any specific elements of the new design, one tool that I have found invaluable in this process has been [Sass][sass], a CSS pre-processor. There are tons of tutorials on Sass and this won't be one of them, but the key improvements I've taken advantage of are variables and functions.

### Typography

I make no claim to any sort of design skills, but one area that I have studied a fair amount of over the years is good typography. [^1]. A while ago I created a [test page][type] that implemented a [vertical rhythm][24ways]. The key aspect of maintaining a vertical rhhythm is to ensure that the line spacing of blocks of text (leading) and the spaces between text blocks or other elements on the page all equal to (or relate) to a specific value. 

Here is a basic example, given a base `font-size` of 16px and a `line-height` of 1.5, our vertical rhythm is 24px. This example will also use ems for sizing type, so 1.0em = 16px.


``` css
body	{
  font-size: 100%  /* = 16px */
}
	
#wrap	{
  font-size: 1.0em;
  line-height: 1.5em; /* 24px */
}
	
p, ul, ol, img, h2, h3, h4 {
  margin-bottom: 1.5em; /* 24px */
}
```
	 
	
If we wanted `h3` headlines to be a larger size, say 18px, we use the formula:

	Desired Em Size = Desired Px Size / Context Px Size.
	
So 18px / 16px = 1.125em. Just setting `font-size: 1.125em;` on `h3` elements would break our vertical rhythm because the bottom margin of the `h3` would no longer be the desired 24 pixels:

	1.125em(h3 size) * 1.5em(bottom-margin) = 1.6875em
	
And 1.675em * the base `font-size` of 16 is 27px. So we have to change the bottom margin of `h3` (and `line-height`) using the same formula:

``` css
h3 {
  font-size: 1.125em;    /* 18 / 16 = 1.125em */
  line-height: 1.333em;  /* 24 / 18 = 1.333em */
  margin-bottom: 1.333em;  
}
```
	
That is all well and good, but if there are more than a few elements with different sizes, that is a lot of math to crank out. When I first started working on maintaining a vertical rhythm, I actually built an Excel spreadsheet to calculate everything:

![screenshot of Excel](/images/vert-rhythm-excel2.jpg)

However, if I decided to change the base `font-size` or `line-height` for whatever reason, I would have to go back and manually change *all* the CSS declarations.

#### Sass to the Rescue.

This is where variables and functions in Sass can make this easy. Here is an extract from the typography section of my Sass variables partial:

``` sass
$base-font  : 16;
$base-lh    : 1.5em;  
$base-vr    : 24;  // 16 * 1.5 = 24px

// Convert Pixels to EMs (Desired = Target / Context)
	
@function em($target, $context: $base-font){
  @if $target == 0 {@return 0}
  @return $target / $context + 0em;
}
```

The `em` function takes two arguments: my desired font-size in pixels and the pixel size of the context it is in. These arguments are variables and the `em` function is declaring both of them: `$target` and `$context`. This latter argument defaults to the `$base-font` variable that I declared in the beginning (which is 16px), if I pass it nothing else. In my redesign, here is the declaration for `h2` elements in my Sass file:

``` css
article h2 {
  font-size: em(24);
  line-height: lh(1, 24);
  margin-bottom: lh(1, 24);
}
```

I've passed a desired size of 24px to the `em` function, which then does the following:

```
@return $target / $context + 0em
  24 / 16 
  = 1.5em
```

I have the `+ 0em` to add em to the returned value since I'm using unitless numbers.

The `lh` function is used to help maintain the vertical rhythm. We'll get to this function in a minute. Here is the CSS that SASS creates for the above `article h2` declaration:

``` css
article h2 {
  font-size: 1.5em;
  line-height: 1em;
  margin-bottom: 1em; 
}
```

With SASS doing all the math, and me doing none, I get the desired font size of 24 px converted to ems, and the line-height and bottom margin are also 24 pixels (1em * 1.5em, which is 24px). And 24px is my desired vertical rhythm. 

A key aspect of a vertical rhythm is that it is a &#8220;rhythm&#8221; and not a rigid scale. Bringhurst writes about deviating from a vertical rythym, but doing so in multiples of the base "leading" or `line-height` in CSS terms. The `lh` function accepts a multiplier as its first argument and the context size in pixels as the second:

``` sass
// Maintain vertical rhythm with Line Height
	
@function lh($amount, $context){
  @return em($base-vr * $amount, $context)
}
```

Here is another example from my Sass typography partial:

```  css
.entry h3 {
  font-weight: bold;
  font-size: em(18);
  line-height: lh(1, 18);
  margin-top: lh(1.5, 18);
  margin-bottom: lh(0.5, 18);
}
```  	

I want the top margin of `h3` elements to be 36px (1.5 * 24px) and the bottom margin to be 12px (0.5 * 24). These add up to 48px, which is an even multiple of the base `line-height`. Let's break this function down a bit.

Remember that the formula for calculating a desired em size is:

	Desired Em Size = Desired Px Size / Context Px Size.
	
Since I have changed the font-size of the `h3` element to 18px, the *context* has changed as well. Manually calculating the margin would be as follows:

```
36px (which is 1.5 * 24) / 18 (new context)
  = 2.0em
```

The `lh` function takes the multiplier (1.5) and the new context (18) as arguments. It multiplies the `$base-vr` variable (which I declared to be 24) by the multiplier (24 * 1.5 = 36) and passes the result as the first argument (`$target`) to the `em` function and passes the second argument (18) as `$context` to `em`:

	@return em($base-vr * $amount, $context)
	
Again, the `em` function is just calculating the Desired Em Size formula: 36 / 18 = 2. The generated CSS for the `.entry h3` declarations is:

``` css
.entry h3 {
  font-weight: bold;
  font-size: 1.125em;
  line-height: 1.33333333em;
  margin-top: 2em;
  margin-bottom: 0.66666667em; 
}
```

The `line-height` passed a multiplier of 1.0 in order to keep it at the baseline vertical rhythm of 24px. If you never need to deviate from this rhythm, the `lh` function is not required and you could just use the `em` function to calculate margins for elements that have different font sizes.

#### WTF?

You could be forgiven for thinking that this is a lot of work, but what if you decide in a week or year to change your default font-size, or vertical rhythm? All that is required to update your initial variables:

``` sass
$base-font  : 18;
$base-lh    : 1.5em;  
$base-vr    : 27;  // 18 * 1.5 = 27px
```
	
Save your Sass file and&hellip;you are done. *Every single CSS declaration* that uses a `em` or `lh` function will recalculate in your updated CSS file. A Google search for 'Sass vertical rhythm' will return a plethora of pre-built functions and extensions that just need to be included in your own files. Or use mine.

#### More Sass Typography Goodness

Designer Mark Boulton wrote [an article][boulton] about incremental leading, which is changing the vertical rhythm of elements with smaller font sizes if the default leading is too large. The new rhythm for these elements is not a complete departure from the base line, but is in sync with it by aligning say every 5th line of smaller text with every 4th line of main text (just read the article if that sounded confusing.) Here is a Sass function I wrote that accomplishes this:

``` sass
// Incremental Leading
// Every 'y' line of affected element will 
// align with every 'x' line of main text
	
@function incr($new-size, $x: 4, $y: 5){
  @return 1em * (($base-vr / $new-size) * ($x / $y))
}
```
	
Let's say we wanted `sidebar` text to be 15px and use the above example values. Here is the Sass declaration:

``` css
.sidebar {
  font-size: em(15);
  line-height: incr(15, 4, 5);
}
```
	
With no more effort on my part, other than to hit 'Save' in my text editor, the following CSS is output:

``` css
.sidebar {
  font-size: 0.9375em;
  line-height: 1.28em; 
}
```
  	
Another area where I have found Sass variables to be helpful is with defining `font-family` groups like so:

``` sass
    $serif-ff:	"ff-tisa-web-pro", Cambria, Georgia, serif;
    $sans-ff: 	"proxima-nova", Corbel, sans-serif;
    $title-ff:	"adelle", Georgia, serif;
    $code-ff :	"DejaVu Sans Mono", Consolas, "Courier New", monospace;
```

Throughout my Sass files I have declarations such as:

``` css
h2, {
  font-family: $title-ff;
  font-size: em(24);
}
	
h3, {
  font-family: $title-ff;
  font-size: em(20);
  font-weight: bold
}
	
/* Couple of hundred lines later...*/
	
.description	{
  font-family: $title-ff;
}
```
	
If I want to change the typeface used for titles, rather than search through my CSS file for all affected elements, I just change the `$title-ff` variable, which are listed right below my other typography related variables. 
  	
Sass has a ton of features such as mixins and the ability to extend CSS selectors, but just using variables and functions has been a huge help in quickly experimenting with different aspects of web typography.

Upcoming articles in this redesign series:

1. Using [Susy][susy] to create fluid grids
2. Colors by [Solarized][solarized]
3. Creating Sidenotes
4. Good web type with [Tyepkit][typekit]
4. Leaving [Movable Type][mt] and the alternatives

[^1]: I can't recommend enough Robert Bringhurst's *[Elements of Typographic Style][bringhurst]* 

 
[lab]: http://www.nealsheeran.com/lab
[home]: http://www.nealsheeran.com/lab/prototypes/home2.html
[single]: http://www.nealsheeran.com/lab/prototypes/article.html
[arch]: http://www.nealsheeran.com/lab/prototypes/archives.html 
[proto]: http://www.nealsheeran.com/lab/prototypes/home.html
[type]: http://www.nealsheeran.com/lab/type.html
[24ways]: http://24ways.org/2006/compose-to-a-vertical-rhythm
[ala]: http://www.alistapart.com/articles/settingtypeontheweb
[tan]: http://v1.jontangerine.com/log/2011/06/ampersand-the-aftermath
[km]: http://kilianmuster.com/blog/the-wonderful-world-of-microtypography-1
[boulton]: http://www.markboulton.co.uk/journal/comments/incremental-leading
[sass]: http://sass-lang.com/
[pin]: http://pinboard.in/u:nbsheeran/
[twitter]: https://twitter.com/#!/nealsheeran
[bringhurst]: http://www.amazon.com/gp/product/0881792063/ref=pd_lpo_k2_dp_sr_1?pf_rd_p=486539851&pf_rd_s=lpo-top-stripe-1&pf_rd_t=201&pf_rd_i=0881791326&pf_rd_m=ATVPDKIKX0DER&pf_rd_r=1NX0M73X6DWC1F1R86SB

[susy]: http://susy.oddbird.net
[solarized]: http://ethanschoonover.com/solarized
[typekit]: https://typekit.com/
[mt]: http://www.movabletype.org