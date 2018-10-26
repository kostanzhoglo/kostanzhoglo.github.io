---
layout: post
title:      "Getting Back to Basics"
date:       2018-10-26 19:20:18 +0000
permalink:  getting_back_to_basics
---


I've been doing some review of the basics this week.  It's funny how much I can take certain basic aspects of languages for granted.  I write functions, assign variables, and console.log multiple times each day.  But looking back and reviewing the specifics of things like *null, undefined, ==, const, let, var, === and more* can be surprising in how much detail is present in the even the most basic of building blocks.  I figured I'd share some quick hits, so come on in, the water's fine!

### == VS. ===
They're both comparison operators.

== is a Loose comparison.  It cares about Value and not about Type.  If I was comparing the following:

`"2" == 2` 
I would get **true** returned.  
The JS engine will look at these two values, and it will convert the TYPE of the primitive data on the right into the TYPE of the primitive data on the left.  In this case, it's changing the integer 2 into a string.  Only **after** the conversion will it compare the values.  2 == 2, so **true** is returned.

=== is a Strict comparison. It cares about Value AND Type.

`"2"===2` 
I would get **false** returned.  
As soon as the . JS engine sees a string and an integer, it already knows they're not equal.  Game over... false!

### var VS. let VS. const
Different ways to assign variables in JS.

**var** is old school, the original variable assigner!  It's been around forever.  
var hoists!
var has *function* scope.  If I have an `if` clause and define a variable inside that code block, it's still accessible within the rest of that function.  It can trip a person up, because I usually think all variables become unavailable outside of a code block, but not so with var.
With var, you can declare a variable at one point, and assign it a value later on.
var also allows for it's values to be *reassigned*.

**let** and **const** are the new(er) kids on the block!  They were introduced in ES6.
Neither let nor const hoist!
They both have *block* scope.  Easier to see where they're available!
Here's where the two newbies differ:
let shares some behavior with var.  You can declare a variable at one point, and assign it a value later on.
let also allows for it's values to be *reassigned*.

const must be declared AND assigned a value at the same time.  It will error out otherwise.
Also, for primitive data types, const can NOT be reassigned a value.
However, a little tidbit to know... If const was used on an object, that value CAN be modified.  It just can't be reassigned.

So, this is ok with const and the JS engine...

```
const newArray = [2, 4, 6, 8]
newArray, push("who do we appreciate?")
newArray = [2, 4, 6, 8, "who do we appreciate?"]
```

### Difference between undefined and null

Both `undefined` and `null` represent empty values.
`undefined` is assigned to variables when they have been declared but not assigned.  So the JS engine is setting that value.
`null` is something I, the coder, will assign to a variable, to clean up a variable in a function that's used a lot.  
I should never assign `undefined` to a variable, because then if I'm testing my code later on, and I get an `undefined` returned back to me at some point, I won't know whether I set that value or the JS engine did.

### Remind me what Prototype Based Inheritance is again?

Basically, every object created in JS has a property called **prototype**.  I can add methods or properties to any object that gets created by that constructor function if I add it to the **prototype** property.  An example will help clarify.

```
const animal = function(name, species) {
  this.name = name
	this.species = species
}

animal.prototype.hello = function() {
  return `Hello, my name is ${this.name} and I'm a ${this.species}!`
}

const john = new animal('John', 'Tiger')

john.hello()
=> "Hello, my name is John and I'm a tiger!"
```

First, I made a new constructor function and saved it to the variable **animal**.
Then I created my prototype function called **hello**.
Because **hello** is connected to **animal**, any animal I now create will have their name and species, which I enter at the time of instantiation, but each animal will ALSO have access to the .hello method.

I mean, who wants an animal who can't say hello and tell you what species they are?!  
Problem solved.


Brushing up on some simple ideas is always helpful, and can sometimes surprise you with a detail you forgot!




