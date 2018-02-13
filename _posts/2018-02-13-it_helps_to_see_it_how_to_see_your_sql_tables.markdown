---
layout: post
title:      "It Helps to See It! How to See your SQL Tables"
date:       2018-02-13 18:35:35 +0000
permalink:  it_helps_to_see_it_how_to_see_your_sql_tables
---


In the months I've been studying coding at the Flatiron School, there are numerous patterns I keep discovering:
--about how I learn new things
--importance of syntax [[those naughty little ( , } . -_ 's! ]]
--testing code is crucial
--awareness of when to take breaks, and length (sometimes looking out a window for 30 seconds does the trick, sometimes a 40-minute run does a similar trick)
		
As I just finished the SQL unit, one of those patterns popped up again: the need to See what I'm working with.  This little sub-pattern fits nicely in the larger "learning about how I learn things."  

Oh SQL, you tamer of data and all things tables!

When first starting the section, I thought it would be lots of eyeballing tables to pull out the data you want, and return it in a nicely wrapped present.  But towards the end of the section, the tables existed (I created them for goodness' sake), and the data was still wrapped nicely, BUT I could no longer see the tables.  This was a by-product of the Flatiron lessons being placed in `.sql` (SQL) files instead of an overall `.db` (database) file.  There's nothing wrong with the formatting, as you can absolutely solve the tests without having a physical manifestation of the data, but I could no longer type `SELECT * FROM characters;` and look at the files I was manipulating.

Knowing myself however, I've learned that it helps me to wrap my head around the problem if I can *See* the tables filled with information.

SO, if you're like me, and Need to See it, here's what to do:

*(Quick Assumption I'm making about you.  I work on a Apple Mac.  So I think you do too.  If that's not the case, some of the below may not work exactly the same way...)*

1) Download a SQL browser application.  Here's a free option that Avi mentions in the review video: http://sqlitebrowser.org/ .  It's a quick download, and I recommend taking 10-20 minutes to familiarize yourself with some of its functionality once you get started.  BUT, to simply see the tables, you can get going in a minute if you like!

2) Complete the portions of the Flatiron Lab where you CREATE TABLE schema, and INSERT your data (otherwise you'll have nothing to OPEN in the SQL browser later on).

3) Then, BEFORE working on the **Query** section of the lab, switch over to your TERMINAL, and create a database file.  I added mine to the Flatiron Lab folder I was working on, but you can add yours wherever is easiest.

`[12:30:21] (master) sql-library-lab-v-000 `

The above is my terminal directory prompt.  **sql-library-lab-v-000** is the Flatiron Lab I was working on.
	 

`$  sqlite3 library_lab_tables.db`

(whatever you name your file, make sure it has the extension `.db` at the end, otherwise the SQL browser won't be able to open it)
	 
	 
	 
4) ADD your tables to the new database file:
5) 
   `$  sqlite3 library_lab_tables.db < schema.sql`
	 
5) ADD your data to the database file:
6) 
   `$  sqlite3 library_lab_tables.db < insert.sql`
	 
6) Ok, now your new database file is full of the info you need.  Time to see it visually.  Go to your desktop or applications folder, and OPEN the SQL Browser you recently downloaded.  For me, that's **DB Browser for SQLite**.

7) Once there, choose OPEN Database, and navigate to the folder where your new database file is located, and double-click.

8) In DB Browser for SQLite, there's an option to BROWSE DATA towards the top of the window you're using.  Click that, and Voila, you can now switch between your various tables and LOOK AT the data you're trying to parse.  


I may not always do this little process everytime I work on a SQL query, but while I'm learning the whole system and figuring out how to grab the bits and bytes I want, Looking at the Actual Info at hand is much more efficient than trying to keep one more thing in my brain.  It's full enough as it is!

I hope this helps as a little guide to quickly see your data.  I'll probably refer back to this to walk me through the procedure when I find myself stuck in a vague haze of "Well, exactly how many apples did Peter eat?  Or was it Oranges?  Or was it Pamela?  I don't even know what I'm trying to return from the query!"

Little operations like the above (remembering the various Terminal Commands to create and add data into files) can trip me up when I'm in the middle of a lab and realize I need to take a look.  I want to keep solving the lab tests, but now I need to go look-up how to create a database file, add info, and open it in the browser.  Eventually, things like this will become second-nature, but for the time being, a little instruction guide will help!

