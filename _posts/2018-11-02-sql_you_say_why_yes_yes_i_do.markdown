---
layout: post
title:      "SQL you say?  Why yes, yes I do."
date:       2018-11-02 19:55:16 +0000
permalink:  sql_you_say_why_yes_yes_i_do
---


Oh SQL!  You wonderful wonderful language that I haven't looked at in months.  HOW ARE YOU?!

Same old same old?

Well, that's just great when I need to review some of your syntax.  Glad nothing's changed!  Never hurts to catch up with an old friend.  That's what old friends do after all!

Sooo, let's jump in to 10 goodies from SQL that I've probably forgotten...

### 1) Get all the info from a table.  And I mean ALL the info.

I have a table of **Users**.  Each User has a **name, ID,** and **email**.
To have SQL return all the info about each user, type:

`SELECT * FROM Users;`


### 2) Basic DB structure.

A DB, or DataBase, is the structure that holds all of the info you want to access.
Columns, or Fields, contain the various types of info you want to store, like **Name, ID,** and **Email** mentioned above.
Rows, or Records, represent each specific instance of data you have.  Each **User** would have their own row in the table mentioned in Point 1) above.

A DB is often NOT just one table, but many tables that RELATE to each other in some way.  (More on this later).
But I find that many times people think a DB is just one table.  It's key to remember / understand, that a DataBase is many tables that can share info with one another.

### 3) I just want Some columns from a table, not All of them...

Well, let's use that SELECT command again, but in a slight different way...

`SELECT name, email FROM Users;`

This will give me just the the Users' **Names** and **Emails**.  Forget those IDs.  Who needs 'em?!

### 4) What if there's repeat info in a column? I only want unique answers!

Say no more, and let me introduce you to DISTINCT.
Let's say there are 7 Users with the name 'Serafina' in our DataBase?  I'm trying to give a pregnant friend some options for baby names.  But I don't want to repeat Serafina 7 times!

`SELECT DISTINCT name FROM Users;`
I'll get back just 1 Serafina (and only 1 of every other name in the DB, no matter how many repeats there may be).

### 5) I need to send an email to Each and Every Serafina in my DB! Help!

No worries, WHERE is here to help.
`SELECT * FROM Users WHERE Name='Serafina';`

I will get back a table with each Serafina, along with their respective email addresses.  

Quick note: Only put 'quotes' around words.  If you were looking for a specifc ID number, just use the number as is.
`WHERE ID=3;`

### 6) What operators can I use with WHERE?

I'm glad you asked!
<
>
<=
>=
=
!=    (not equal)
BETWEEN     (in a range)
IN  
LIKE
AND 
OR
NOT

### 7) Are AND, OR and NOT special?

They certainly are!
They're used with WHERE to be more specific and add other conditions to your query.
AND will only return answers where both conditions are true.
OR will return answers when any of the conditions are true.
NOT will return answers when it's False!

`SELECT * FROM Users WHERE NOT Name='Serafina';`
Looks like everyone not named Serafina is gonna get an email!

### 8) Wait, can I combine AND OR NOT operators?

Why, yes, yes you can.

`SELECT * FROM Users WHERE Name='Serfaina' AND (City='Los Angeles' OR City='San Diego');`

They lost my mail to California friends whose name begins with Seraf.  Thank goodness I can use SQL to quickly find the friends I need to resend season's greetings!

### 9) Welcome to Good Burger, can I take your ORDER?

ORDER is used to arrange your results from your query in a specific placement.

`SELECT * FROM Uers ORDER BY Name;`


The default for ORDER is ASCENDING (or ASC), which is smaller values first and bigger values last.  You'd have to specify DESCENDING (or DESC) to have it ordered the other way.
`SELECT * FROM Uers ORDER BY Name DESC;`

### 10) What if I want to get a little complex with my ORDERING? Mayo on the side I say!

Sure, we can do that.  Check this out...

Let's order our Users by Name, and the City where they live.

`SELECT * FROM Users ORDER BY City, Name;`

Now I'll get the Users from Albany (in alphabetical order), then the users from Boston (in alphabetical order), then the users from Chicago (in alphabetical order) and on and on.

Ok, great, but can it get even crazier?!

It sure can, try this one out...

`SELECT * FROM Users ORDER BY City ASC, Name DESC;`

With this QUERY, I'll get the Users from Albany (in **reverse** alphabetical order), then the users from Boston (in **reverse** alphabetical order), then the users from Chicago (in **reverse** alphabetical order) and on and on.


### Ok, those are 10 quick SQL hits.  Is that the whole shebang?  NO WAY.  But 10 is enough to ponder / think on for now.  Come back next week to discover INSERT INTO, UPDATE, DELETE and a slew of others!
