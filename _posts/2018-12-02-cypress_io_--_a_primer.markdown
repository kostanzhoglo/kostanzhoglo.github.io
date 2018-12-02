---
layout: post
title:      "Cypress.io -- a primer"
date:       2018-12-02 12:34:33 +0000
permalink:  cypress_io_--_a_primer
---


Ahh, testing!  Ensuring that your program actually works the way you intend it to.  A step that is skipped too often, but is vital for robust code that holds up its end of the bargain.

[Cypress.io](https://www.cypress.io/) is a new tool for me, and boy am I glad I found it.  Or rather, boy am I glad it was part of a coding challenge for a recent job application!  Let me show you some of the features, and I'm sure you'll be setting aside some time to look further into it on your own (it made testing SO easy for me!)...

### Install and Set Up

You'll need node and npm installed and ready to go on your computer.

Once you're in the project directory you'd like to test, **install Cypress**:

You can either add it directly to your `"devDependencies"` in your package.json file, or in your terminal, write `npm install cypress --save-dev`.

(This will take a little bit of time.)

Once installation is complete, Cypress will give you some instructions in the terminal on how to start it up: 

`You can now open Cypress by running: node_modules/.bin/cypress open`

Instead of having to write that each time you want to start it up, I found it easier to write this shortened script in my **package.json**

```"scripts": {
    "cypress": "cypress open"
  }```
	
Then I only had to type `npm run cypress` and the program would start.
	
### What happens when Cypress runs?

A new folder will be created in your project directory, the **Cypress** folder.  Cypress will also kindly alert you to this same fact in a new dialogue window that will help you run your tests.  In that dialogue window, after hitting "OK", you will see the `example_spec.js` file.  Clicking that file will run the tests in your browser of choice, and you can watch the tests happening on your app side by side.

PLEASE NOTE: You must have your app server up and running before telling Cypress to run its tests, you'll be looking at a blank screen and some error messages.

If you run the `example_spec.js` file you'll see a great amount of tests being run, and seeing all those tests go Green.  The world is a wonderful place!

### But let's write some of our own tests!

If you've ever written test files before, some of this syntax will be familiar!

You write your tests in files placed in the **cypress/integration** folder.  Create whatever new file names make you happy.  A good description of what functionality they are testing will make you even happier later on...

For instance, if I was making a recipe app, where a user could create, find, update and delete recipes, here's a beginning test file for the `app-start.spec.js` file...

```describe('App starts', () => {
  it('Loads recipes on page load', () => {
    cy.server()
		cy.route('GET', '/api/recipes', seedRecipes)

    cy.get('.recipe-list li')
      .should('have.length', 3)
  })

  it('Shows an error on failure', () => {
    cy.server()
    cy.route({
      url: '/api/recipes',
      method: 'GET',
      status: 500,
      response: {}
    })
    cy.visit('/')

    cy.get('recipe li')
      .should('not.exist')

    cy.get('.error')
      .should('be.visible')
  })
})
```


To explain a little:
`cy` is written to use Cypress library of commands.

`cy.server()` spins up the server in the test file so you can make http calls to specific addresses.

`cy.route()` defines the Request you want to handle.  Param1 is the http verb, Param2 is the URL, and Param3 (optional) is the response object you're sending.
You can also set up the website `status` if you like (which I needed to do to make sure I got the error response I was looking for in my 2nd test).


Who helped me figure all of this stuff out?!  Well, the Cypress docs were invalubale, found at **https://docs.cypress.io/guides/overview/why-cypress.html#In-a-nutshell**.

Also, there is an amazing tutorial you can find on youTube at **https://www.youtube.com/watch?v=KfTH2d-JZ6k&list=PL8GlT7H3xOcJbXNVnM6lTT3Fec8dikotY&index=2&t=0s**.
Shout out to **Andrew Van Slaars** for putting that tutorial together and making it so clear!!


Seriously, if you've never used it, go check out Cypress.io this week when you have 10 free minutes.  (And no, I'm not getting paid to by them to write this.  Just a believer!)
