---
layout: post
title:      "CORS Deep Dive"
date:       2018-10-12 17:24:23 -0400
permalink:  cors_deep_dive
---

## Why am I writing this?
I was working on a coding challenge this week, and I needed to create a simple web page and fetch data from a recipe search-engine API on a different  domain.  One of the first things I wanted to nail down in the challenge was the data request.  

Below is the code I was using to make my request.  (DISCLAIMER: the names of the API website has been changed to protect the innocent.)

```
  getRecipes = (userInput) => {
    fetch(`https://www.DEFAULT_recipe_WEBSITE.com/api/?q=${userInput}`)
      .then(res => res.json())
      .then(response => {this.setState({ recipes: response.results})
      }
    )
  }
```

I fired up my app to test whether the fetch request was working. I decided to search for recipes with *carrots* as an ingredient, but after submitting my query, to my dismay, in my browser console this error popped up:

**Failed to load http://www.DEFAULT_recipe_WEBSITE.com/api/?q=carrots: No 'Access-Control-Allow-Origin' header is present on the requested resource. Origin 'http://localhost:3000' is therefore not allowed access. **

The above is a CORS error.

## What is CORS?
CORS stands for, Cross Origin Resource Sharing.

Let me break it down a little bit.  

**Origin** - any domain. 
     www.facebook.com
		 www.buzzfeed.com
		 www.chase.com

**Resource** - any API endpoint that could share some data.  If MLB.com had an API with stats from all professional baseball games ever, and I wanted to send a data request to MLB.com/api (that's a made up website) to find out how many strikeouts Sandy Koufax had in 1958, that data is the Resource.

Ok great, and why does CORS exist?
In the olden days of the internet, if you opened some website, say, www.don't_trust_me.com, read an interesting article, and left that tab open while you remembered you had to make sure you had enough money in your bank account to pay a bill and opened www.chasies_bank.com to double-check, you would be potentially putting yourself in a risky spot.

On its surface, www.don't_trust_me.com was a treasure trove of interesting, buzzy articles, but underneath it had some code scripts running and waiting for you to hopefully open another window or tab in your browser.  When you opened your bank website and signed in, now www.don't_trust_me.com could request info about your account number, address, or worse yet, try to make a transfer, unbeknownst to you.

To fix the above problem, Web Browsers (Chrome, Safari, Firefox, etc.) put some security protocols in place.  Namely, you could only request data from the same Origin (website) that created the request.

With that security in place, using the example above, www.chasies_bank.com would only accept requests that also started from www.chasies_bank.com.  If www.don't_trust_me.com, it would get the same error I received up top!

To make a long story short, Cross Origin Resource Sharing was a no-no.  This protected innocent people browsing the web, unaware of dastardly criminals motives and actions.

However, you may have a very good reason to want to request some info from a different website.  For me, www.DEFAULT_recipe_WEBSITE.com/api is a free API to search and retrieve data from.  But I'm still getting blocked because of the security protocols!

## What to do!?

Luckily, there are various workarounds to solve this problem.

If I was in control of www.DEFAULT_recipe_WEBSITE.com/api, I could white-list certain websites that I trust.  But this wasn't an option for me.

If I was using a back-end framework (like Rails, or Django, or etc.) there are gems and packages (like rack-cors) that alleviate this problem, and send your data request with the correct headers to allow CORS.

But because this was for a coding challenge, and I didn't want to add all the code for a back-end yet (as I had no current need to save data locally), I was looking for another way.

And through my searches I found two websites that do the same thing.  They proxy my request, so my request will get green-lit by the www.DEFAULT_recipe_WEBSITE.com/api server.

Here's the two websites to check out, and I'll show my code as an example for how to implement it:

1) https://cors-anywhere.herokuapp.com/

2) https://cors.io/

If you take a quick look at those websites, they're pretty bare bones, but they explain what they do and how they can help pretty fast.  Basically, if I tack that website to the URI I'm requesting data from, it sets up the correct request headers, so that the browser won't put up the red light and give me an error.

Here's my new code:

```
getRecipes = (userInput) => {
  fetch(`https://cors-anywhere.herokuapp.com/http://www.DEFAULT_recipe_WEBSITE.com/api/?q=${userInput}`)
    .then(res => res.json())
    .then(response => {this.setState({ recipes: response.results})
    }
  )
}
```
	
And when I typed in "carrots" again and tested it out, everything worked perfectly, and the new recipes showed up fine.
	
I highly recommend using either of those proxy websites **if you're in development of a new app**.  You have to make sure you trust the website you're trying to get data from.  If your app was live, I would go a more secure route that you have more control over.  

Happy data requesting!
