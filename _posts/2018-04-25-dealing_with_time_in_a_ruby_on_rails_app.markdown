---
layout: post
title:      "Dealing with Time in a Ruby on Rails App"
date:       2018-04-25 15:42:06 +0000
permalink:  dealing_with_time_in_a_ruby_on_rails_app
---


Ok, here's the finishing touch for my Ruby on Rails Project... the blog entry!

There's an immense feeling of accomplishment in completing this project.  There's a LOT of material covered and many different requirements to handle.  And figuring out how to get all those i's dotted and making sure your program doesn't break in a myriad of ways is very satisfying.  I can't quite believe I built this thing from scratch (and by scratch I mean with the enormous help of those who created and built out Rails along with dozens of other gems, lines of code, snippets, etc.).  I thank goodness that so many before me have asked thoughtful questions and received nuggets of wisdom from the coding community.  Finding the right answer sometimes takes a while, but reading up on all of those wonderful resources is time well spent.  The spirit of generosity is very healthy, and much appreciated!

My app, [remember_your_run](http://https://github.com/kostanzhoglo/remember_your_run), is  a basic log your run program.  I've loved running since I was a little kid.  And for me, one of the enjoyable aspects is marking down what I did, and seeing progress and mileage build up over time.  Of course there are Many apps just like this, built into phones and other wearable technology.  But I'm very happy with my first foray into figuring out how to log all of this specific data and crunching some numbers to make the math easier on the user.  A tricky aspect of measuring speed on a run (if you're not wearing a watch or using a device that tells you) is that you have to know your time and distance.  And then you have to perform some interesting math (which all depends on how much you enjoy doing math).

The basic format if you're doing it in your head is as follows:

1) Get the **Total Seconds** of Your Run (Minutes * 60) + Seconds  
2) Divide **Total Seconds** by your *Total Distance to get Seconds / Mile  
3) Divide Seconds / Mile by 60, to get Minutes Per Mile.  
4) The Remainder from Step 3 is the Seconds Per Mile.  

For example, if I went on a 4.3 mile run in 30:18 minutes, the breakdown would be something like:  
1) 30 * 60 = 1800.          1800 + 18 = **1818** Total Seconds  
2) 1818 / 4.3 ~ 423 (rounded)  
3) 423 / 60 = 7 Minutes   (remainder 3)  
4) 3 Seconds left over.  

My average pace was 7:03 per mile for my run.

Now, that math is fun for me to do during my cooldown after a run.  But it's not everyone's cup of tea!

Well, figuring out how to accomplish that math through a computer program involved lots of knowledge I've gleaned over the past months.

Here's some of the code that helped me get my final answer:

``` 
def total_seconds(entry)
    time_array = entry.split(":").collect {|index| index.to_i}
    if time_array.count == 2
      total_seconds = (time_array[0] * 60) + time_array[1]	
    elsif time_array.count == 3	
      total_seconds = (time_array[0] * 3600) + (time_array[1] * 60) + time_array[2]		
    else	
      total_seconds = time_array[0]		
    end	
end
```
	
The above helper method only covers step 1 of the process outlined above.  I have 3 more helper methods to get me to the final answer.  But this is enough to dissect.  

The user enters the duration of their run as a string "30:18".  I need to split that string into an array, turn them separate indexes into integers, and then perform the math to get my Total Seconds, accounting for seconds, minutes, and even hours, depending on the runner.

Then the return value of this helper gets passed into the other helper methods.  I think it must be fun for the computer too, since it never complains about all the computations I give it.

This project brought a lot of things into focus for me though.  When you're learning the minutiae of a new coding language, you wonder when you will use these new tools, or which ones you'll even remember because so Much info is being pushed into your brain.  But this assignment reminded me that it's all in there, and to trust that I know how to solve these problems.  Sometimes it takes 20 (or 30 (or 40)) minutes to remember the regex pattern, or that it's first(5) instead of limit(5) in this language.  But it feels great when you solve the bug you didn't realize you created.

And now, on to JAVASCRIPT!!

