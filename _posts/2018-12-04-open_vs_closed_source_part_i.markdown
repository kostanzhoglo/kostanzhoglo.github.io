---
layout: post
title:      "Open vs Closed Source, Part I"
date:       2018-12-04 18:13:16 +0000
permalink:  open_vs_closed_source_part_i
---


This is really the 3rd installment of my tech glossary series.  Here are Parts [1](http://jeffreywithers.com/i_o_lamp_mean_and_the_acronym_throwdown) and [2](http://jeffreywithers.com/glossary_throwdown_part_ii).

I was reading a job description today that said "Basic knowledge of Linux OS is a plus."  Even though I have been coding for more than a year now, and know that Linux exists, and MacOS and Microsoft are different (not to mention any other OS that's out there), I don't know where these different Operating Systems came from and why.  So, I figured, let's do some research and dive in, and we'll add some terms to the glossary as we go along...

Oh goodness, there's a LOT to read up on about this topic.  I guess because eventually it goes back to the beginning of all  operating systems in the first place.  There are LOTS of acronyms and lawsuits.  I have a feeling my first stab at this dark corner of the computing world will have some info I may have to correct later on.

Still though, I must be brave and forge on!

### Source Code
A programming language that humans can read.  This is in contrast to **binary machine code (1001001110101011)** that I wrote about in Glossary Part 2.  An **assembler** or **compiler** takes the `source code` and translates it into **machine code** and then your program runs.

Source code is still an abstraction of course.  If you've never studied computer programming before, looking at a basic `for` loop may still not necessarily make complete sense.  But learning coding is like learning any foreign language.  Eventually, you'd be able to read it like any language.  **Binary machine code** on the other hand, not so much.  

### Why am I discussing source code vs. machine code you ask?

**Because it's the sticking point on the great OPEN SOURCE vs. CLOSED SOURCE debate in the software world.**

If I write a computer program and show you the source code (which is OPEN SOURCE), you could study the functionality of what I wrote, and modify it.  

**What's wrong with that?**

Nothing at all, inherently!  However, there are 2 scenarios where it becomes problematic.  1) If I'm trying to make money off my program by selling it to others.  And 2) If I don't trust your motives (or am just very paranoid).  What if you use my program for evil purposes!?  

**Oh, I see.  Well, why share it at all then?**

Well, because sharing knowledge is a good thing.  It's egalitarian, and it allows others to build upon your work.  Having 30 minds (or 30 million) work on solving a problem is better than having 1.  More bugs will be fixed, the program will run more efficiently.  What's that phrase (I'm going to paraphrase and murder it here.)... ? *"If you want to go fast, go alone.  If you want to go far, go together.*

## Beginning of Closed Source code (for computers anyway)...

In 1971, two employees at AT&T's Bell Labs, Ken Thompson and Dennis Ritchie, published the first manual on UNIX (Uniplexed Information and Computing Service).

AT&T licensed the source code for those who could pay for it.  And it was expensive!  If you couldn't buy the software, you couldn't see what they built.  Too bad for you!

## Beginning of Open Source code 
Who has the kind of money to buy an expensive program like UNIX?  Universities!

And **University of California, Berkeley** was one of those universities.  Now, software programs are living, breathing things (metaphorically speaking).  They're constantly being edited, refactored, given a haircut and a shave.  

The developers at **Berkeley** and **AT&T** kept working on their UNIX code, independently of each other.  AT&T eventually released the version of UNIX, **System V** in the 1980s for commercial sale.  Again, quite expensive to purchase.  Berkeley eventually re-wrote / updated all of the old source code they purchased in the 1970s, and released a FREE version of UNIX called **BSD -- Berkeley Software Distribution**.  

Whoa, wait.  FREE?  Yes, that's right, Free.  

Why?

Becuase they're a university and are trying to share knowledge! (I assume.)

What's important to note at this point is that people are still trying to figure out how to make money off these new powerful tools called Operating Systems.

Idea #1: Closed source. Sell them executable files which they can run and work well.  If you try and open the file, it will look like the crazy 01011011 line after line after line.  Infuriating!

Idea #2: Open source.  Show your code for free.  Then sell companies the *Support* they will need to integrate and run that code efficiently.  

Here's a better way to say the above from the documentary **[The Code](https://www.youtube.com/watch?v=XMm0HsmOTFI)** - a sort of history about Linux (which I haven't even gotten to yet!)...  

***For Red Hat, it wasn’t important that we ship a better OS than Microsoft’s or Sun Microsystems’ — it becomes really important that we ship an OS that solves a problem for our customers that they cannot solve [themselves] using the traditional proprietary “binary only” software (MSFT, Oracle). We were recoginizing what we were doing was we were building technology and then giving it away. So we said: “Well, how do you make money doing this?”  Of course, we would go to California to Silicon Valley and everyone said: “Well you cannot make money in the software business by giving your technology away.” We would come back and talk to our customers and we realized the only thing that kept our customers loyal was that we did give away our technology.  For the very first time they had control over the technology they’re using.***
~Robert Young, CEO Red Hat, Inc.


***The real value in most software products is the active maintenance down the line — the continuing support relationship between the vendor and you.  That’s what gives software fundamentally the characteristics of a service industry rather than the manufacturing industry.***
~Eric S. Raymond (ESR)


The documentary is informative, so check it out.  But definitely turn on the Closed Captioning!

Also, Gary Sims has a great [video](https://www.youtube.com/watch?v=jowCUo_UGts) explaining a lot of this stuff.  But maybe wait until part II of this comes out, so there are no spoilers!

Ok, I'll leave it here for now, and pick it up with the next portion of this story.  Fascinating how it all came about!





















