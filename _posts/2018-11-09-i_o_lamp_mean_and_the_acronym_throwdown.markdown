---
layout: post
title:      "I/O, LAMP, MEAN, and the Acronym Throwdown"
date:       2018-11-09 16:09:20 +0000
permalink:  i_o_lamp_mean_and_the_acronym_throwdown
---


So many different acronyms.  Technology is a vast world, made up of people who love to save time.  Thus, the revolution of abbreviations and codewords was born!

As I'm learning more and more about this industry, I find I spend a good amount of time learning these new phrases and shortenings of languages, technologies, hardware and software.  I figured it'd be helpful to keep a glossary of sorts, both to firm them up in my own brain, and as a resource for others.  This is by no means exhaustive, but I will keep adding things from time to time.  There's a lot of these things!  Also, quick note.  Basically, each of the terms I'm discussing here could be their own (or many) blog posts of their own.  This is just to give a quick hit, ya know, to keep you fresh and current!

### I/O
Input / Output.

Everything involving a computer is either **Input** or **Output**.  It's a pretty simple idea, but can get tricky, depending on the perspective you're coming from.
From a human perspecive, a Keyboard is Input (type in some letters), and a Monitor is Output (see those letters appear on the screen).
However, from a computer's standpoint, a Keyboard has output in the form of code signals from the keys tapped by the human.  The computer takes those Output signals and uses them to input into other processes (opening applications, allocating Memory, etc.).

Paramaters passed in to a function?  Input.
Return value from same function?  Output.

### LAMP
**L**inux / **A**pache / **M**ySQL / **P**HP

**Linux** is an Operating System (O/S).  It's the base layer, the overall environment that everything else rests on top of.
**Apache** is web server software.  It's a liaison between your computer (desktop / laptop / phone) and the computer where the files for a specific web page (nytimes.com, zillow.com, etc.) are kept.  It **serves** your computer those requested files.
**MySQL** is a database.  It holds on to information for specific users (emails, names, passwords) as well as data on a website (election results, how many interceptions Tom Brady throws).
**PHP** is a scripting language.  It allows you to manipulate the data on web page, performs all functionality (buttons, forms, video).

LAMP is known as a Stack.  It's the software that, when used together, brings full functionality to a website.
Another Stack is the...

### MEAN
**M**ongoDB / **E**xpress.js / **A**ngularJS / **N**ode.js

**Node.js** is the web server software.
**Express.js** is a light framework on top of Node which gives the developer many built-in methods, allowing a person to write shorter code to do more.
**MongoDB** is the database.
**AngularJS** is the front-end framework.  It's the design elements you see when you go to Wikipedia or abc.com.

MEAN is another Stack.  The main advantage (I think) of MEAN is that all of its parts can be accessed by Javascript.  Also it's a non-binding I/O stack, making it less memory-cumbersome.

### Blocking vs. Non-Blocking Scripts

Blocking means that whatever script is being run, needs to be downloaded, parsed, and executed, before being able to move on to the next bit of code.

Non-blocking, also known as asynchronous, allows for the browser to move on to the next bit of code (script B) before script A is finished running.  How could that happen you say?  Well, a Really oversimplified answer would be this:

When you go to a website and ask for some data to be returned (like your past workouts from a Fitness app), that data needs to be retrieved from the server computer that holds onto it for you.  By being **asynchronous** a non-blocking script moves on and lets you, the user, do other things on the page (start a video, enter info on a form, etc.) instead of being forced to wait for the data to come back about your workouts first.

This is a good start for some glossary items.  But in truth, I see what a can of worms I've opened up.  So many more to hit.  Until next time!
