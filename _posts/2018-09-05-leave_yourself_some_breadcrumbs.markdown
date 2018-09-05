---
layout: post
title:      "Leave Yourself Some Breadcrumbs. "
date:       2018-09-05 17:11:02 -0400
permalink:  leave_yourself_some_breadcrumbs
---

## Some tips on solving your React-Redux Project

This feeling I'm having, it's a little crazy.


I just finished my React-Redux FINAL project for the Flatiron School.  It's just dawning on me what that means, and what is coming up next in my journey as a computer programmer.  When first starting out at Flatiron and imagining what it would feel like at the end of this process, I didn't know what kinds of new knowledge I would have, or how expertise occurs in this field.  


And now, here I am, and there's this sort-of-crazy-feeling, where I know how much I've learned and how amazing it feels to be able to look at code I've never seen before and be able to follow the logic and see the various bells and whistles.  And at the same time, to know that the coding world is ***Always Coming Up With Something New*** where I will need to jump into new paradigms and patterns on what seems like a weekly basis, in order to expand my world and keep up with the new technologies.  It's the push-pull of getting more expertise in languages I already know versus the feeling of discomfort and excitement of jumping into the deep end of new language.  It's very exciting to UNDERSTAND how things work.

But, back to my React-Redux final project.  There's a few points I'd like to highlight about my work on this project.

## Let your variable be breadcrumbs, to give you hints along the way!
## As told through combineReducers(), fetch and other variables...

During some labs in Flatiron, but especially when I was working on my projects, I found that I would run into very similar variables.  The same thing happened in this project.  When I'm in the middle of trying to solve an issue and I'm running into variables like `state.workouts.workouts` it doesn't always help for me to start figuring out where each of those "workout"s is coming from.  It happened to me when I was trying to get my workouts array to render to my component.  When I saw the double up of words, I start to wonder where exactly in my app is the bug coming from.  Is it "workouts" or "workouts"?  

I think it's only an issue for me now, when I'm still a relative new person to React and Redux.  I know how important it is to learn the conventional naming patterns of various languages, so you can catch what the code is trying to hint you towards, but at the beginning, I realize now, I need to name my variables with slight variations on a theme, so it will tip me off when I have a bug, as to where I need to look.  

For instance, in my **reducers/index.js** file, the convention is to name the property of your reducers value after that reducer, as such:

```
import { combineReducers } from 'redux';
import workoutsReducer from './workoutsReducer';

export default combineReducers({
     workouts: workoutsReducer
})
```

But, when my workoutsReducer also returns a `workouts` array, then I'm running into a line of code like this: `state.workouts.workouts`.  That code is 100% correct, but when I run into a bug, it takes me that extra bit of time to figure out which workouts is which.  To help myself out, I wrote my combineReducers like this:

```
export default combineReducers({
     allWorkoutsState: workoutsReducer
})
```

Is it a little longer to write?  You bet. 


Does it help me to see `state.allWorkoutsState.workouts` when I'm trying to solve a problem?  You bet.

I used this same trick when I was getting my return value from my fetch promises.  I know the convention is to simply write:

```
.then(response => response.json())
.then(response => dispatch({ type: 'GET_WORKOUTS', workouts: response.workouts }));
```

But seeing those repetitions of **response** again and again gets me into that trouble spot.  I find that code is easiest to work through when I can say the sentence in my head (or out loud if no one's around!).  But, saying "response to response, json method gets me the response to dispatch the action where workouts equals the response workouts," frankly makes my brain fuzzy.  Instead, I used:

```
.then(response => response.json())
.then(workoutsResp => dispatch({ type: 'GET_WORKOUTS', workouts: workoutsResp.workouts }));
```

Is it a new revolution?  Absolutely not.


Does it give me a little more context, to remember which variables go where?  Yes indeed.


Using the above breadcrumbs helped me solve a problem where I had to follow the bug from my action ---> to the Rails database ---> to the redux store ---> and then finally, to see that the issue was in my parent container component passing down some faulty props to my presentational component.  Every breadcrumb helped!

## P.S. namespacing your Rails backend to "api"

One other hiccup I had during this process was that I namespaced my Rails side to "api".

**config/routes.rb**
```
Rails.application.routes.draw do
    namespace :api do
        resources :workouts
    end
end
```

Again, having "api" as part of the URL for my endpoints clarified the process for me.
BUT, the small part I forgot was that I had to Create an **api** folder in my project to hold my workouts_controller.

When I was first trying to pass an action to create a new workout and persist it to the database it took me a good 15 minutes of trying to *code* the solution, until I realized that the "code" I needed was that parent folder to hold my workouts_controller in.

Just figured I'd pass this along!

It really feels incredible to have finished this project.  And I like using the app as well, so that's a nice bonus.
The truly inspiring thought for me though is to know the learning has only begun.  Very much looking forward to going deeper, being curious, and helping others!
