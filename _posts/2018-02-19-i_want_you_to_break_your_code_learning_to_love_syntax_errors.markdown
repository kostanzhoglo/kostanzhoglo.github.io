---
layout: post
title:      "I Want You to Break Your Code: Learning to Love Syntax Errors"
date:       2018-02-19 16:39:08 +0000
permalink:  i_want_you_to_break_your_code_learning_to_love_syntax_errors
---


It's a unique sort of joy when you replace a `}` with a `)` and all your tests go green.

Or when you realize you had `))` but really needed `)))`.  

Or the time you couldn't understand why you were getting these crazy errors when all you were trying to do was call the 
`#my-favorite-extra-special-method-ever`
only to remember it's actually
`#my_favorite_extra_special_method_ever`.

Early on at Flatiron there are some lessons about the importance of reading error messages and understanding what they're trying to tell you.  I couldn't agree more, and it took me a little time to realize just how helpful errors can be.  That they are letting me know where I need to look, and some hints about how to solve the issue.

I suspect you too are convinced about the power of errors and how helpful they are, but just in case you still need some convincing (or if you'd like to delve into some specifics about errors and the helpful tests that look after you), here's two videos reviews from Avi Flombaum that helped me *Immensely*:

1)[ Collaborating Objects - Pure OO with TDD - LV Lecture](http://https://www.youtube.com/watch?time_continue=205&v=iYcQ693LXck)

The video is over an hour long, but here's the pertinent parts about errors and tests:
   2:45 - 15:00     Creating tests for your program
	 15:00 - 22:00  Building out a custom error message "AssociationTypeMismatch Error"

2) [Debugging a Tuff One in Music CLI](http://https://www.youtube.com/watch?v=J_BSGPW37AE)

This video is 26 minutes long.  All really good error review, but especially:

0:00 - 4:00       Working backwards thru light-blue error messages to see where the break is originating

10:00 - 15:00  Separating out Which method is failing
	 
However, the types of errors I really want to discuss today are SYNTAX ERRORS (and one other strange error types).  You know, the ones where you truly break your entire program.  You don't even get the pleasure of seeing the red-test-fails, only the light-grey of Terminal basically saying "You didn't even write your *programming language correctly*, forget about testing out the logic."

The first time I hit a syntax error (Instead of the regular test failures from rspec), it really threw me, because it was such a strange new world.  So, what I decided to do was to get more familiar with them, by *intentionally* breaking my code after completing a lab.  I know that once you finish a lab, the desire to immediately click on "Next Lesson" is strong, but what I'm telling you to do instead, is Breathe, Wait a Second, and see if there's one or two things you can learn about your shiny new code before leaving it for the next challenge around the corner.

Look, your code works, the tests say so!  

But This Moment is the Perfect Time to look at a few easy break-points, so you can look at the errors coming from a calm place, instead of when you're in the throws of trying to solve the tests, don't know what you're doing wrong, and the panic-level is starting to rise.  

So, instead, do the following:
   1) change the white-space on a command (or place a , . ( [, etc in a new spot )
   2) save the file
   3) run the test suite again
   4) see what, if anything, broke
   5) READ the error message carefully

The beautiful thing about the above process is that you ALREADY know exactly how to fix the error.  So you can look at the error message objectively, instead of bringing your emotions into it.

I really use this method when I'm starting out on a new language.  It's a perfect time for me, since I just finished the SQL section, but am still learning the ins and outs of where white-space is allowed, and where it's not.

Here's a few examples of what I'm talking about.

```
CREATE TABLE users (
  id INTEGER PRIMARY KEY,
  name TEXT,
  age INTEGER
);
```
Works perfectly fine.  BUT, add an accidental comma after `age INTEGER,` and ALL 22 tests from my lab FAIL.


Using heredoc,

`sql = <<-SQL`

Is good to go.  BUT, add a space between <<- and SQL, i.e. `sql = <<- SQL` and your tests fail.



One more example: in the dynamic-orm-lab, some code is present when you begin in the student.rb file:
`require_relative "../config/environment.rb"
require 'active_support/inflector'
require 'interactive_record.rb'

class Student < InteractiveRecord

end`

So, before even starting this lab in earnest, I played with some of these lines of text, to see what might break, and what those errors look like.

**Deleting ".rb" from the require lines:**
`require_relative "../config/environment"
require 'interactive_record'`

NO effect, all my tests are still passing.  Good to know!


**Deleting < InteractiveRecord**
`class Student`

One lab test failed now, but syntax still works ok.


**Deleting Student < InteractiveRecord**
`class

end`

Broke the program.  The classic error "syntax error, unexpected keyword_end" showed up.  Understood!


**Deleting all of       class Student < InteractiveRecord end**

So, only the require and require_relative lines were left.
The error I received back was interesting.  The program didn't break, but I the error message was:


     NameError:
      uninitialized constant Student
     ./spec/student_spec.rb:3:in '<top (required)>'
    No examples found.

    Finished in 0.00032 seconds (files took 0.40455 seconds to load)
    0 examples, 0 failures, 1 error occurred outside of examples


This is the kind of error that could throw me for a loop in the middle of a lab or project. 

0 examples?

0 failures?

1 error outside of examples?

In the middle of working on the lab, I might delete or comment out something inadvertently and find myself facing this error message.  But now, after practicing how to break my programs in various ways, I get used to seeing some strange messages, and can recall when I've seen them before, and have some leads as to what I did to put myself in this spot.

So, I'll certainly keep spending a couple minutes every week looking for ways to safely break my code, so I can deepen my understanding of why and when certain error codes appear!  I highly recommend it!










