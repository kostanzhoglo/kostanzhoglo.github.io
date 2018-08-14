---
layout: post
title:      "Careful Mr. Wayne... (Scope & Hoisting in JavaScript)"
date:       2018-08-14 14:32:04 -0400
permalink:  careful_mr_wayne_scope_and_hoisting_in_javascript
---


One of the most important things I've learned in coding is if you don't know what your functions' return values are, you're in a lot of trouble.

And in order to know what your functions are returning to you, you have to know what values your **variables** represent.  This can sometimes be tricky in JavaScript due to issues with *Scope* and *Hoisting*.  

To help clarify this discussion on Scope and Hoisting, Batman is going to help me out.  Yes, that's right, Batman.  Secret identities always raise the stakes (and help me understand when I want to keep a variable protected, or when it's ok to share info with the world at large).

A few things to note before diving in to some examples, 
* *it matters how you declare a variable.  Variables behave differently depending on if you use **const, let, var** or **no keyword** to declare them.*  It's always safest to use **const** and **let** at this point.  You'll find yourself in hot water if you decide to use **var** or **no keyword** at all.
* each example below is *separate and isolated *from every other example.  Any variable declarations are set *only* in that example.


1) Any variable declared outside of a function has Global Scope.  This means all my functions will have access to it.  

```
const identity = "I'm Bruce Wayne"
    // => undefined

identity
    // => "I'm Bruce Wayne"
		
const lateDinner = () => {
    return `Dinner was delicious, and ${identity}.`
}

lateDinner()
    // => "Dinner was delicious, and I'm Bruce Wayne."
```

Even though **identity** is declared outside of the function `lateDinner( )`, it's still available inside the function.  Bruce enjoyed a meal, and made no faux pas.



**~Scope Chain Interlude~**
What's happening here is that if a function references a variable that is not declared INSIDE that function, JavaScript will look for the value of that variable in the **Scope Chain**.  When `lateDinner()` is called, at first Javascript can't locate what **identity** means.  It will immediately look to the next outer Scope to see if the variable-in-question is declared there, and it will continue doing this until it gets to the GLOBAL SCOPE and searches there as well.  If the variable is never declared along its **Scope Chain**, you'll get an error message.

An image that helps me understand Scope Chain are those [Russian Matryoshka Dolls](https://en.wikipedia.org/wiki/Matryoshka_doll).  They're nested dolls, one inside the other.  If a variable is *referenced* in the innermost doll, but is NOT DEFINED there, JavaScript will look to see if that variable is defined in the next doll up, and then the next doll up, etc., until it finally searches for that variable value in the GLOBAL context.

For instance, the tiny grandchild doll may want to eat some **soup**, but the grandmother doll is where that **soup** variable is defined.  JavaScript will continue looking for the value to **soup** until it finds the answer in grandma's brain.
**~Interlude Over~**




2) Any variable declared inside a function is NOT available outside of that function.  Variables declared inside a function have **LOCAL SCOPE** to that function.

```
const identity = "I'm Bruce Wayne"

const boardMeeting = () => {
    const company = "Hot Dogs R Us"
		return `Yes, we should buy ${company} immediately, and ${identity}.`
}

boardMeeting()
    // => Yes, we should buy Hot Dogs R Us immediately, and I'm Bruce Wayne.
		
company
    // => ReferenceError: company is not defined       !!!!!!
```

If you're lucky enough to be in the Board Room meeting, you know which company Bruce has his eye on.  However, to the general public (i.e., GLOBALLY), no one knows what **company** Mr. Wayne wants to buy.  The variable has LOCAL SCOPE only to the **boardMeeting()** function.


3) Going back to the **Scope Chain**, even if you declare and define the same variable inside and outside a functiuon, as soon as the JavaScript engine finds a suitable value for the variable, it will stop looking up the Scope Chain.

```
const identity = "I'm Bruce Wayne"

const fightingCrime = () => {
    const identity = "I'm Batman"
		return identity
}

fightingCrime()
    // => "I'm Batman"
```

I defined **identity** twice here, but as soon as JavaScript found the value inside the function, it looked no further and sent back the return value.  Thank goodness, 'cause I need Batman fighting crime, not Bruce Wayne!


## Hoisting!
Let's dive into some **Hoisting** while we're at it.  Hoisting occurs because JavaScript has two phases, the *compilation* phase and the *execution* phase.  

During the Compilation phase, the JS engine will store declared functions and variables in memory.  It won't store their values, just that they exist.

During the Execution phase, JS looks for the values of the functions and variables.  

These two phases can create some bizarre behavior in JS when running code.  Let's see if we can clear up some confusion.  An important thing to remember with Hoisting is that **var** is the keyword that can really get you into trouble here.  **const** and **let** will also technically get hoisted, but they will throw an Error when hoisting becomes troublesome.  The tricky aspect of **var** is that it won't throw an error, but will simply return `undefined`.  Examples will help you see what I mean...

4A) Hoisting in action with **var**

```
function iAmBatman() {
  console.log(identity)
  var identity = "I'm Batman"
}

iAmBatman()
    // => undefined       (console log)
       undefined
```

When calling `iAmBatman()`, the first line printed above is printed to the console.  The final line is the actual return value of the function.

Let me break this down a bit.  
**Compilation Phase**  JS notes that there is a function `iAmBatman()` and a variable `identity`.  But it is only noting that they *exist*.  Their value at this point is undefined.

**Execution Phase** JS will execute the code line-by-line, In Order.  So, when it gets to `console.log(identity)` it will print out **undefined** because that is still `identity`'s value leftover from the Compilation Phase.  No error is thrown, because **undefined** is a valid value in JS.  

Basically, JS, sees the above code as:

```
function iAmBatman() {
    var identity
    console.log(identity)
}
```

So currently, Bruce Wayne is trying to confess to us his big secret, but all he's able to say is "undefined".  Let's fix this a bit, yes?

4B)
```
function iAmBatman() {
    console.log(identity)
  var identity = "I'm Batman"
	 console.log(identity)
}

iAmBatman()
    // => undefined       (console log)
		  I'm Batman     (console log)
          undefined
```

JS sees the code from 4B as:

```
function iAmBatman() {
    var identity                                    DECLARATION
    console.log(identity)
		identity = "I'm Batman"                     ASSIGNMENT
		console.log(identity)
}
```

Well, that's a little better.  Bruce can finally tell us who he is, after he stammers out "undefined" at first.

HELPFUL HINT

But the way to *truly* fix this is to place any variable declarations and definitions at the TOP of whatever scope you're in, whether that be Global or a local function.  It's a best practice to avoid confusion, and always let Bruce Wayne speak from the heart.  Here's an example:

4C)
```
function iAmBatman() {
    var identity = "I'm Batman"
    console.log(identity)
}

iAmBatman()
    // => I'm Batman     (console log)
          undefined
```

The return value of "undefined" is happening because that's the default return value of any function.  You can easily solve this by writing `return identity` directly underneath `console.log(identity)` in example 4C above!


To reiterate, Hoisting can create quiet bugs in your code when using **var**.  **const** and **let** will also be hoisted and cause problems if you don't declare them at the top of any execution scope, but at least **const** and **let** will throw an error and tell you that a mistake is happening.  **var** on the other hand, will simply place "undefined" in your code, without throwing an error.  

In summary, here's my best advice regarding hoisting (and helping Batman keep Gotham safe):

###### I) Never use **var** whenever you can help it!

###### II) Always declare variables at the TOP of any scope, whether it be inside a function or globally.  It will steer you clear of any hoisting troubles.

Good luck out there!


