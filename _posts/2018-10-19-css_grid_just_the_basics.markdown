---
layout: post
title:      "CSS Grid, Just the Basics"
date:       2018-10-19 18:18:08 +0000
permalink:  css_grid_just_the_basics
---


This week I started working through Wes Bos' course on [CSS Grid](https://cssgrid.io/).  I've only worked through the first 3rd of the course so far, and I think I should be finished by next week.  But I wanted to share some of the tips I've learned so far, that I have a feeling I'll be using a lot more in the coming weeks, months, years...

Oh, also, before I forget, the course is well laid out, FREE, and seriously helpful!  Wes is a Really clear teacher, and doesn't make assumptions about what you know.  He sidebars and explains other ancillary concepts that will help you gain a deeper understanding of the subject material.  I highly recommend the course!  He even has an [AMA](https://github.com/wesbos) (Ask Me Anything) GitHub page, and answers tons of questions very quickly.

### Set Your CSS Colors as Variables
You can set the palette of your main colors right from the get go, making it easier to style and them your page.

In your main .css file (or really any .css file you wish):

```
:root {
  --purple: #870bed;
  --gold: #f9e316;
	--white: #f7f6f2;
}
```

And then to use in your project, still in your .css file:

```
html {
  color: var(--gold)
}
```

Simple as that.  But will help keep your colors standard, with no fuss over remembering the hex-code to get the same continuous look.

### Download the Firefox Developer Edition when doing CSS Work
In the beginning of the course, Wes recommended downloading the Firefox Developer Edition program.  I've been a Chrome convert for years now, and am accustomed to those devtools, so I had to be convinced, but it **Didn't Take Long**.  

As soon as you open the console, go to the **Inspector** tab and in the sub-area on the lower right, choose the **Layout** tab, and it's beautiful, well-organized, and lets you dissect the page to really see what space you're working with, and what you've explicitly designed already, and which areas allow for more flexibility.

In the future, I'll be using this browser when doing anything CSS.  I'll probably devote a future post about the devtools on their own.

### Grid, just the basics
This portion is just the basics, just the basics.

To get started, all you would need is some HTML using a parent element of class="container" and however many children elements of class="item" you wish.

The CSS is:

```
    .container {
      display: grid;
      grid-template-columns: 200px 400px;
      grid-template-rows: 150px 100px;
      grid-gap: 30px;
      grid-auto-rows: 150px;
    }
```

`display` is just to alert the browser you'll be using **grid** instead of **flex** or some other configuration.

`grid-template-columns` or `rows` sets the length of those respective elements, and how many of each you would like.

`grid-gap` is the space set aside between the various grid boxes.

`grid-auto-rows` will set the height of future rows you might add after the specifically delineated rows you account for in `grid-template-rows`.   For instance, if you have the above `grid-template-rows: 150px 100px` and end up using 10 "item" elements, the first 4 elements will be put into the first two rows (because each row has 2 columns (hence 2 columns * 2 rows = 4 elements total)), which leaves you with 6 extra "items" to place correctly.  By using `grid-auto-rows` the browser now knows to place 2 "item"s per row, and each extra row should have a height of 150px.


I've never found organizing web pages to be this easy, so I'm psyched to continue along and finish this up next week!

And good news, according to [Can I Use](https://caniuse.com/), CSS Grid is supported on almost 88% of browsers, so whatever you're creating will be seen as you intended almost everywhere.

Happy gridding!
	
