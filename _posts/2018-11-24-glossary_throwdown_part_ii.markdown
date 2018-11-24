---
layout: post
title:      "Glossary Throwdown, Part II"
date:       2018-11-24 16:27:00 -0500
permalink:  glossary_throwdown_part_ii
---


I started this glossary a couple of weeks ago.  To see the first installment, click [here](http://jeffreywithers.com/i_o_lamp_mean_and_the_acronym_throwdown).

There's lots of info that people may take for granted you understand and are well-versed in when operating in the software engineering world.  But, I need to check my ego at the door, and make sure I've read up on and understand some basic terminology and paradigms, so I don't get ahead of myself.  If you're like me, then this post is for you!

### Machine Language

This is what the computer actually reads and understands for its instructions.  It is the most basic computer language.  What's it made out of you ask?  Well, you know how we use the decimal number system (we count 0-9, before introducing a 2nd digit in "10"?).  In Machine Language, it's a **binary number system** which means you count 0-1 before introducing the next digit.  

Machine language looks like this:

0110100100100000001101011010101111010010001111010010110010010011111


Wheeeee!!!


At the most basic level, every decision is either YES or NO.  **0** is NO.  **1** is YES.  
The light bulb is either OFF or ON.

By using many different decisions ALL at once, you can achieve some pretty amazing functionality.  I'm talking Super Mario Kart here.  (And I think that was only 32-bit at the first iteration.)

### What is a bit?  What does 8-bit vs. 64-bit even mean?

A **bit** is built off of Machine Language from above.  Every digit is a bit.  A bit can either be 0 or 1.  So in this example,

`0110` 


There are 4 bits.  In fact, that string of `0110` is a 4-bit number.  

Using that idea, that means that an 8-bit number looks like this: `10010111`.

& a 64-bit number looks like this: `1001001010010010100101001001001010010010100101001001001010010010`.

I hope this helps (it helped me).  I'm going to count to 10 with the decimal system, and with the binary (bit) system.  Side by side.

00     0000
01     0001
02     0010
03     0011
04     0100
05     0101
06     0110
07     0111
08     1000
09     1001
10     1010

Does that help a litte to visualize it?

### So what's so important when you go from 8-bit to 16-bit?

Well, if you can give a computer 8-bits of info at a time, that means you can specify among 256 different options.  Wait, let me simplify a little.  Remember our counting to 10 above, using the binary system?  I needed 4-bits to do that, since "ten" was `1010`.  Let's pretend we only had 3-bits to work with. `000`.

If we only had those 3 spaces, we can only make 8 different total options, like so...

000
001
010
011
100
101
110
111

Every time you add a new bit, you double the number of options available.  Add a 4th bit?  16 options.  5th bit?  32 options.  6th bit?  64 options.  7th bit?  128 options.  8th bit?  256 options.  Hey we got back to the number at the top of this section!  

Are you starting to see the pattern above?

Yes, that's right it's 2 to the power of however many bits you have available in your computer.
2 to the 4th power?  16.
2 to the 8th power? 256.
2 to the 16th power? 65,536.

That could be the difference of having 256 crayola crayons to doodle with, or 65,536 crayolas!  BIG difference!

### Wow, gotcha.  And a bit is a byte, ryte (I know it's really spelled right.  Kids, it's spelled 'right'!) ?

NO, a byte is **8 bits**.  

Why on earth is a byte 8-bits?  Why isn't it 6-bits or 7-bits?  
Sadly, I don't have a great answer for you, but I have a feeling it's 8 at least in part because 2 cubed is 8, and mathematicians (and computer programmers) like that sort of thing.  2 to the 7th power doesn't have as nice a ring to it.

A byte size has been standardized since the 1960s.

Why is spelled byte and not bite?

Because they didn't want people accidentally spelling bite when they meant to write bit. bYte helps avoid that headache.

### Ok, one last question. A Kilo-byte is 1000 right?  I mean, a kilogram is 1,000 grams, so of course it's the same thing in computer land.  Right?  

Wrong.  Sadly, a Kilo-byte is actually 1024.

WHAT.  WHAT.  WHY???

Well, again we're coming back to that binary language paradigm.
2 to the 10th power doesn't cleanly come to 1000.  It comes to 1024.

Since 1024 is **pretty close** to 1000, computer scientists when with KB.

### So that means MB (megabyte) isn't exactly 1,000,000 either?  What about GB (gigabyte)?  What about TB (terabyte)!??

Oh, definitely not Exactly 1,000,000.  But roughly, pretty darn close!  Don't be sad, it's just how computers are!

And GB and TB are even further off, but again, PRETTY CLOSE to the numbers you think they are!



Ok, this completes Round 2.  You can see what going down the rabbit hole gets you.  I meant to write this post about **compiled vs. interpreted computer languages** but that will have to wait until Round 3!


