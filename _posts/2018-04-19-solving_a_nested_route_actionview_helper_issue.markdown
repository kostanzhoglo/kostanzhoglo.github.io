---
layout: post
title:      "Solving a Nested Route ActionView Helper_ Issue"
date:       2018-04-19 17:54:16 +0000
permalink:  solving_a_nested_route_actionview_helper_issue
---


This is a debugging post.  It's pretty specific, but I wish I had found an article like this earlier today before spending 90 minutes trying many different solutions with little success. 

Shout-out to Luisa Scavo for helping me get to the correct code!

Quick background: I'm working on my RAILS Portfolio Project. It's a fairly simple log-your-run app, since that's something I wish I had a lot of days.  Input your distance, time, any intervals, etc., and it saves the data, gives you an average speed, etc.

The problem: My Month's "show" web page served a couple purposes: 1) You can log a new run, and 2) You can see your previous runs from that month in a table.  

When creating a new run, it's already associated with the month that it belongs_to (so, a nested form_for).  Here's the code setting that up:

path: views/months/show.html.erb

```
<%= form_for([@month, @run]) do |f| %>
  <%= f.label :date %>
  <%= f.text_field :date %>
```

	
The form gathers much more info, but that's the pertinent code.  @month is the Parent, and @run is the object you're creating (and assigning info to) in this form. 
	
Further down the page I list that month's previous runs taken by our user. As an added feature, the date of each run is a LINK so the user can see just the info for that run in isolation on it's own show page.  Here's the page setting all of that up:
	
path: views/months/show.html.erb

```
<% @runs.each do |run| %>
   <tr>
      <td><%= link_to run.date, month_run_path(run) %></td>
      <td><%= run.name %></td>
```

Aaaand, before showing you the error I received and the mystery that ensued, here's the last part of pertinent code, the #create action from my Runs_controller:

```
  def create
    @month = Month.find(params[:month_id])
    @run = @month.runs.build(run_params)
    if @run.save
      redirect_to month_path(@month)
    else
      @month = Month.find(params[:month_id])
      @runs = @month.runs
      render 'months/show'
    end
  end
``` 

The above code made sure that my Run object was going to be instantiated with an association to its parent Month.

This morning I was testing validations on the #create action.  Basically I was in this part of my #create code:

```
    else
      @month = Month.find(params[:month_id])
      @runs = @month.runs
      render 'months/show'
    end
```

When I failed to properly validate my form fields, I was *Expecting* to render the months/show.html.erb page again with error messages popping up in my form, guiding me to what I did wrong.  

INSTEAD, I received this error message:

```
ActionController::UrlGenerationError in Runs#create

Showing /Users/jeffreywithers/Development/code/remember_your_run/app/views/months/show.html.erb where line #52 raised:

No route matches {:action=>"show", :controller=>"runs", :month_id=>#<Run id: 1, date: "2/1", name: "Shore Dr.", distance: 4.2, duration: "30:00", pace_per_mile: nil, notes: "Cold outside. Great running weather.", number_intervals: 3, interval_length: ":40", rest_between_interval: "1:30", created_at: "2018-04-18 22:05:11", updated_at: "2018-04-18 22:05:11", month_id: 2, user_id: nil>}, missing required keys: [:id]
```

This is my line 52:

```
      <td><%= link_to run.date, month_run_path(run) %></td>
```
			
I read the error, trying to parse exactly what it was telling me:

1) This error was for previously created objects (because it was in the display portion of the page, not the form)

2) My display portion was working BEFORE my creation validation tests (i.e., the links were working to various run Show pages)

3) The error was telling me I was missing a **required :id key**. (Very end of error message)

4) In the first line of the error message I could see the **month_id** was "#".  Which confused me, especially since the run object itself HAD a **month_id value of 2** (last line of error message).

Ok, so what do you think went wrong?
Take your time, no rush.

I figured the problem was the ActionView helper method prefix **month_run_path** so I tried different variations on that, but nothing worked.  Here's where Luisa came to the rescue.  She asked me, what is the URL path that **month_run_path** is helping to get you to?

Easy enough to answer...  "rake routes" in Terminal, and for that particular one you get:

```
/months/:month_id/runs/:id
```

And she asked me, "How many arguments do you need to supply to get to that route?"

And it all clicked.  I had only been passing 1 argument to the helper method!  I needed to pass both the run AND the parent month!

This is the code that solved the problem.

```
month_run_path(run.month, run)
```

The little bit of extra credit is that you can't simply supply "month" as the first argument.  It has to be month in relation to your run, hence **run.month**.

Ok, hope this helps someone else in the coding universe!  For now, I'm diving back into my Rails Project!


