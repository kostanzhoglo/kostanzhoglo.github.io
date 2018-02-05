---
layout: post
title:      "My CLI Gem Project: Healthy Foods!"
date:       2018-02-05 15:23:26 +0000
permalink:  my_cli_gem_project_healthy_foods
---


Hello hello!  Good to see you out there, it's been a while.

This entry will cover my journey of creating my CLI gem, Healthy Foods.  It will have its ups and downs, but the important thing is that I finished it, And I learned that I know more than I give myself credit for (and that I have to learn Much Much more)!

Coming up on this project, you hear about the stress and fear of others who have gone before you.  It feels like a dangerous task.  Will you make it through unscathed?  Will you upset anyone near you while you're coding because you're cursing (or crying) loudly?

When I read the initial learn.co README, I realized I would need to read it another two or three times.  There are a lot of instructions, and I wanted to make sure I wasn't missing something important.  The BIG takeaway from this entire project is that if the tasks are broken down, I can tackle them.  But I (and I think many other coding beginners) get ahead of myself and view the Entire Project at once, and that's where the stress becomes dangerous.

So, reading the initial instructions (and re-reading and re-re-reading them) helps to remind me to take it one step at a time.  

So, step #1?
Watch the walk-through of Avi thinking through a demo CLI gem project.  It's a little over an hour long, but there's a ton of helpful info in there, that it took longer as I was writing copious notes, and marking any questions I had as he went through.  Thank goodness for the ability to pause and go back!

Helpful takeaways:
   * he kept the theme of 'one step at a time.' going strong
   * he writes notes to himself in the #methods; reminders about the goal of that #method
   * he made the program work at first with fake (hard-coded) data, then went back later and programmed it correctly.
      **This was most important for me.  Easy to get lost in abstraction, especially when your program breaks.  But if you keep adding in literal examples of how the program *should* function, you can at least see where the errors are breaking your code, AND it helps you Visualize what you actually want.**
	
Step #2
Create a repository on github for the project.
I created my project directory locally first, and used the helpful tutorial from [Rails Casts, episode 245: New Gem with Bundler](http://http://railscasts.com/episodes/245-new-gem-with-bundler?autoplay=true).  It's a 7-minute video and Very helpful!  The following line of code creates your entire gem directory for you.  

```
$ bundle gem healthy_foods
```

Step #3
Create the CLI gem.  The main event!
The entire first portion of this was dedicated to getting the right required dependencies working amongst the various folders and files. 

I leaned heavily on Avi's video walk-through during this part, as I'm not well versed in the requires and the require_relatives of the world yet.  Avi moves fairly quickly, but if you take your time, and watch carefully, you'll see when the require is in healthy_foods.rb instead of bin/healthy_foods.  
Something I continue to wonder about moving forward and being curious about best practices are the number of folders and files that basically have the Same Name.  For an example of what I mean, here's some of my project file structure:

**healthy_foods** (directory)
     -bin
		       -healthy_foods (executable)
		 -lib
		      -healthy_foods
					     -cli.rb
							 -food.rb
							 -version.rb
				  -heatlhy_foods.rb
					
It took me some time to get used to various functions of each healthy_foods file or folder.  I wonder if this is standard practice in the coding world?

Once the requirements were set correctly, and the executable **healthy_foods** was getting me to cli.rb correctly, the issue of coding the actual program began.

I already noted it above, but the big lesson I learned in doing this project was how important it is to make your program work, even if it's using simple "puts" and printing out hard-coded data.  If I didn't watch Avi's awesome tutorial, I would never have followed that path.  I don't know why I would want to make it harder on myself, but a pang of "That's not a real program, it's populated by fake hard-coded lines." would have been running in my head.  Foolish thinking.

Following Avi's lead, I kept writing in the data about bananas, carrots and black beans, knowing I would fix it later.  And I felt different than I had on some previous projects.  I felt momentum build more easily, even as I struggled with certain portions to fix my broken code.

BECAUSE, when I ran the program, and I saw bits and pieces working, the overall effect of what I wanted to build kept me in the game.  Otherwise, without the visual of seeing what the eventual project would be, I could've gotten lost in the morass of "I can't even really see what's breaking."  From here on out, when I'm coding, I'll be putting literal phrases and functionality in, even if I'm faking it at first.  

Ok, to make this blog post not a true novel, here's a few tidbits from completing this project, and how I got through some of the tougher errors I was coming up against:

1) It MATTERS where you place your *binding.pry* when testing return values!
     This is more of a note for binding.pry, but forgetting this fact jammed me up for a good 30 minutes or so, when I couldn't tell why I kept getting the error "undefined local variable or method...".  I finally realized it was because I placed my binding.pry Outside of a loop in my code, and couldn't access the local variable info inside.  Once I placed the binding.pry Inside the loop, I could look at the return values I needed.  
		Here's an example of what I'm talking about...
		First, here's the MISTAKEN binding.pry placement:
		
```
food_page.css("div.slot-6-7-8 div div div").each do |div|
  food[:serving_size] = div.css("div").text.gsub("1.00 cup(", " ").gsub(")", "")
  food[:calories] = div.css("div").text.gsub(/.+[)]/, "").gsub(/[GI]\S+\s+\S+\s\S+/, "")
end
binding.pry
```

When I tried to see the return value of food[:serving_size], by typing in this to my console prompt  ```div.css("div").text.gsub("1.00 cup(", " ").gsub(")", "")``` , I got the **undefined local variable or method...** error.  


However, when I re-placed my binding.pry Inside the method, as below...
		
```
food_page.css("div.slot-6-7-8 div div div").each do |div|
  food[:serving_size] = div.css("div").text.gsub("1.00 cup(", " ").gsub(")", "")
  food[:calories] = div.css("div").text.gsub(/.+[)]/, "").gsub(/[GI]\S+\s+\S+\s\S+/, "")
  binding.pry
end
```


I was able to look at the return values I needed.  Felt great to remember that lesson!

2) I kept getting Namespace errors because I was referring to other classes and methods incorrectly.  
     I am new to using Namespace::Class.method names when calling on methods inside a small program.  I kept forgetting the original Namespace attribute.  This was a fairly easy fix, as the errors were pretty clear as to what was going wrong.  
		 
I was calling methods like Food.all instead of HealthyFoods::Food.all.

A little refactoring cleared this up.

3) Regex was killing me.  Regex is a great tool.
     The website I was scraping from was full of valuable info, but the formatting of the html and css was not helpful.  There were very few `class=names` and instead most of the website was built with `divs` upon `divs` upon `divs`.  It was difficult to grab the info I wanted, and *just* the info I wanted.  But with enough trial and error with regex (and looking up about a dozen stackoverflow answers) I finally wrangled together the regex patterns I needed!  The best lesson here was to remind myself that "I can figure this out.  Don't get down on yourself."
		 

Looking back over this project, I can't believe how much I learned, and the feeling of accomplishment is surprising.  

Onward an upward!

(and now to look back over the code a couple more times and make some extra notes to remember everything I did!)





