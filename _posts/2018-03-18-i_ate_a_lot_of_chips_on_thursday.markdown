---
layout: post
title:      "I Ate a Lot of Chips on Thursday..."
date:       2018-03-18 21:10:53 -0400
permalink:  i_ate_a_lot_of_chips_on_thursday
---

## A Sinatra Portfolio Project Tale

I will make this brief.

I will try to make this brief.

Test-driven development is an excellent way to work on a project, but I didn't have the tests I've come to rely on in the regular bootcamp labs.  The portfolio projects are a bit like the wild west, in that you're coding without many warnings when you're going over a cliff.  You'll write some code, and then check your program, looking for weird behavior, or if you've really gummed up the works, you'll get a syntax error or a Sinatra error.  I ran into all of these (as expected) while creating my Sinatra web app, [Read_It_Later](https://github.com/kostanzhoglo/read_it_later).  

This is a tale that has been told many times before, of what happens when a really sticky error piles up, and can take you to that dark place, and how you get back out of it.

To give the littlest of backgrounds, **Read_It_Later** is a bookmarking app, where you can save articles into custom topic folders, and read later when you have more free time.  You can also peruse other users articles, and perhaps find new or common interests with others (most likely family or friends, since they'd have to be saving articles on your local version of the program).

A User has_many topics, and a Topic has_many articles.  Simple enough.

On Wednesday I built out all the CRUD functions for Topics, along with the Views, as well as the sign-up, log-in, log-out functions for users.  It took me time as I ran into the "I forgot to add the @ in @topic there" or "I rendered the wrong page from that controller action."  But it was good, solid progress, and I had hopes of finishing up the whole program on Thursday.  I knew Thursday would be a Bit more complex since I was adding the extra layer of Articles, and I would need to think through how to add and edit those along with connecting them to Topics and Users at the time of creation or alteration.

But then, Thursday happened, and I entered the coding Twilight Zone.  I was working on my route when receiving from my form to create a new article. Here's what my form looked like from views/articles/new.erb:

     <h1>Create a New Article</h1>

     <form action="/articles" method="post">
       Article Title: <br>
       <input type="text" name="title"> <br><br>
       Full Web Address: <br>
       <input type="textarea" name="url"> <br><br>

       Which Topic Folder should this Article be placed in? <br>
       Please -EITHER- <br>
       Choose an already existing Topic Folder: (only choose one) <br>
       <% current_user.topics.each do |topic| %>
          <input type="checkbox" name="topic_id" value="<%= topic.id %>"><%= topic.name %><br>
        <% end %> <br>

       - OR -
       Write the name of a new Topic Folder: <br>
       <input type="text" name="name"> <br>

       <input type="submit" value="Make New Article">

     </form>

The crucial line of code from above is,          
```
<input type="checkbox" name="topic_id" value="<%= topic.id %>"><%= topic.name %>
```

I needed this line to match up correctly with my post '/articles' action, which is below:

       post '/articles' do
    if params[:title] == "" || params[:url] == ""
      flash[:message] = "Error. You can't leave Article Title or Web Address blank. Please try again."
      redirect '/articles/new'
    else
      @article = Article.create(title: params[:title], url: params[:url])
      if !params[:name].empty?
        @article.topic = Topic.find_or_create_by(name: params[:name])
        @article.save
        @topic = @article.topic
        @topic.user = current_user
        @topic.save
        redirect "/articles/#{@article.slug}"
      else
        @article.topic = Topic.find_by(id: params["topic_id"])
        @article.save
        @topic = @article.topic
        @topic.user = current_user
        @topic.save
        redirect "/articles/#{@article.slug}"
      end
    end
  end

The real line that was killing me here was:  
```
@article.topic = Topic.find_by(id: params["topic_id"])
```


I needed the "topic_id" of the form to match the params["topic_id"] of the action.  Now, the above code I've written is the correct code.  But I kept getting error after error with small changes I was making to those two lines.  At first it's not so bad, because there are lots of things you can try.  A bracket here, a parentheses there.  But after you've cycled through those options (and other variations) two, seven, twelve times, you start to wonder if something else is going wrong...  "Yes, I've read the error message from Sinatra, and it's telling me where the errors are happening.  But sometimes error messages aren't perfect and I can't help but wonder if some other dependency at a different point is the real culprit."

Once doubt about your code creeps in, the Coding Twilight Zone has been entered.

As I mentioned, since I don't have tests, all I can do is change a little snippet of code, and go into the browser itself, fill out the form, and cross my fingers that it either succeeds, or I at least get a new error message.  But again and again, and again, I get similar errors (or the Exact Same one) no matter what I try.  

So I did what any normal person I do.  I ate my feelings.  I ate my panic.  It would happen more often in the beginning of this coding adventure.  When you look at the error message you're getting, and you wonder what could POSSIBLY be wrong?  You read and reread and reread each line of code, letter by letter, to make Sure it couldn't be a syntax, or misspelling error causing all the ruckus.  There's a desire to laugh.  There's a desire to cry.  Because at points you doubt your sanity.  Haha!  Hahahahhaaa!

And of course, in the end, you find the one '/' you left out.  Or that '@topic' needed to be 'topic' in this method.  And then some guffaws, sighs, and warm relief comes over your entire body.  You're not crazy after all.

In those dire moments, I find that chips help best of all.  There was a large Trader Joe's tortilla chip bag that paid the price for this error on Thursday.  They served their duty deliciously.  

I made an appointment with a technical coach for that evening, since I really had tried everything I could think of.
I kept trying to solve the issue before the meeting, as I really wanted to solve and move on, but no luck.
Dakota Martinez was my coach that night.
I explained the issue, and he suggested we dive in to the form.

When the meeting began I was on the error page from Sinatra in my browser.
So I clicked the back arrow to take me to the page before, had my binding.pry set up and ready to go in the controller to catch the params, and was about to hit submit again, when Dakota said (I don't remember *Exactly* what Dakota said, but this is the gist), 

"Oh, you need to refresh the page."  

"What?"

"You need to refresh the page for the form, or the browser will only resend the same data from before.  The browser will use what's in its cache if you don't refresh, so you won't send new data.  Any time you update the html in your code, you need to refresh the form page, so the browser loads the alterations."

"WHAT." 

Cue the laughter from my end.

"Oooohhh, oh no, I didn't know that.  I have a feeling I may have written the correct code at some point and wasn't refreshing correctly, so THAT's why I was getting the same error message over and over."

More laughter.


Now, I'm sure I DID refresh correctly sometimes and had the code wrong instead at certain points.  But not knowing about the refresh need definitely screwed me up for several hours on Thursday.  But, well, ya know, ya learn something every day. !

Dakota helped me work through the issue expertly, peppering me with questions so I was getting to the right answers myself.  His advice was always pushing me to answer the questions:

"What is the return value of that?  If you're getting that error, where is the info coming from?  Where's the first place you should look if it returns that value?"

It made me think of something Avi says a lot in the video reviews:
(Again, paraphrasing) "In ruby you're always calling methods on objects, or you're setting a variable.  That's it."

Thursday was finished with solving of that bug.  I left the Coding Twilight Zone and moved into Friday.

Several more serious issues popped up with editing my articles, and making sure a user couldn't alter anyone else's content.  At one point I accidentally wrote over the info for EVERY article object each time I updated one.  Then I did it three more times before I caught on to what was happening.

But following the guidelines from Dakota, and Avi, (and confidently Refreshing forms when I needed to) had me solving all the bugs that came my way.  What was the error message telling me exactly?  Where should I look first?  What do I think the return value is?  Is that the return value I'm getting?  Those are all pillars of debugging.  And slowly but surely, they're sticking in my brain more and more.

I learned a TON from this project.  And even though error messages can at times be painful, they're the most useful part.

I'm excited to jump into the Rails section, but before I exit Sinatra, I'll leave you with this beautiful poem I thought of today...

**Autobiography in Five Chapters**
by Portia Nelson

I     I walk down the street.
There is a deep hole in the sidewalk
I fall in.
I am lost...
I am hopeless.
It isn't my fault.
It takes forever to find a way out.

II     I walk down the same street.
There is a deep hole in the sidewalk.
I pretend I don't see it.
I fall in again.
I can't believe I'm in the same place.
But it isn't my fault.
It still takes a long time to get out.

III     I walk down the same street.
There is a deep hole in the sidewalk.
I see it is there.
I still fall in...it's a habit
My eyes are open; I know where I am;
It is my fault.
I get out immediately.

IV     I walk down the same street.
There is a deep hole in the sidewalk.
I walk around it.

V     I walk down another street.



