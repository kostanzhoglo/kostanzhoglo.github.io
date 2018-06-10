---
layout: post
title:      "Active Model Serializers Give Easy Access to Object Methods as Attributes"
date:       2018-06-10 17:29:18 +0000
permalink:  active_model_serializers_give_easy_access_to_object_methods_as_attributes
---


This post details one small portion of Rails / jQuery project app, [**remember_your_run**](https://github.com/kostanzhoglo/remember_your_run), which I finished earlier this morning.  For most of my blog posts, I've been trying to write articles that I wish I had found when I was working on the project.  The hope is, someone (a future version of myself perhaps) will be better able to find some info about an issue that snagged me for a while as I was working through the app.

My app helps runners keep track of the runs they went on, and the important data points for each.  I've been a runner all my life, and am always searching for easier ways to track progress, and see when potential injuries might be creeping up.  I've been using an earlier version of this app for a month now, and it's great to see when my calf soreness began, or the average pace per mile of my runs per month.  Helps me see when I need to take it easy, or switch up my running workouts.

A User has_many months in this app.  A new month is created through a form where a User enters the name, year, and a goal for the month.  However, I want my month object to track other cumulative info as well, but it's info that could not be entered at the time of creation: things like total mileage for the month, and average pace of all the runs combined during that time frame.  So, to give me that data, I created Month object methods `#month_mileage` and `#month_pace`.  

The problem I ran into (pun intended), was when I wanted to access those pieces of info when accessing my JSON object from my new API endpoints (the main goal of this project).  It was my understanding that Active Model Serializers grabbed the attributes of an object and serialized it for you into a JSON object from which you could grab the data points you wanted to display to the User.  But how to access return values from a method, I wasn't sure.

I posted in one of the slack channels, and a kind person gave me a tip on using the `to_json` method.  But the syntax for that `to_json` can become messy quickly, and I went through a good hour of trying to get all the curly brackets, "only"s and "includes" in the right order before figuring there must be a better way.  And of course there is. Cernan Bernardo (**Shout out to Cernan!**  So knowledgeable and clear when explaining!) explained the solution this way:

> Because your serializer is essentially attempting to call a method for each object that is being serialized via the attributes, you can just add `month_mileage` as an attribute and it will attempt to call that method for each month and return that value in the json

Of course, it all made sense, but I still have a bit of skepticism that something like magic can occur in Rails.  Here's the code that worked perfectly:

```
class MonthSerializer < ActiveModel::Serializer
  attributes :id, :name, :year, :goal, :month_mileage, :month_pace
  has_many :runs
  belongs_to :user
end
```

I went to the URI to see my months info JSON page, and there it was, **month_mileage** & **month_pace**, neatly summed up along with my other data points in my May 2018 JSON object.  

I added those bits of info to the jQuery display function after the AJAX call was finished, and moved on to tackling my next issue.  

And now, on to the last sprint in my Flatiron School program!!

