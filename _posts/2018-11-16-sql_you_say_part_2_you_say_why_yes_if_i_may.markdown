---
layout: post
title:      "SQL you say? Part 2 you say? Why yes, if I may!"
date:       2018-11-16 11:18:38 +0000
permalink:  sql_you_say_part_2_you_say_why_yes_if_i_may
---


Find Part 1 of this series over [here](http://jeffreywithers.com/sql_you_say_why_yes_yes_i_do).

Part 2 starts immediat—

### 11) SQL, I had 3 Best Friends yesterday, but I made a new Best Friend today. How do I add this newbie into my Friends table?!

`INSERT INTO table (col1, col2, col3, col4)`
`VALUES (val1, val2, val3, val4)`

`INSERT INTO Friends (name, type, email, age)`
`VALUES (‘Marty’, ‘Best’, ‘mmcfly@outtatime.com', 45);`

Type that query, and Marty will be one of your best friends in no time.

### 12) How does NULL work in SQL? 

`NULL` does not care for =, >, <.  You have to use `IS NULL` or `IS NOT NULL` instead.  It will check if that field for that record is empty (hence, Null).

`SELECT col_names FROM table WHERE col_name IS NULL;`

`SELECT UserName, Address FROM Users WHERE Address IS NULL;`

Notice, you should display a column that is not the column where you're searching for the NULL value.  That way, you have info to *reference* where the NULL value is appearing.

### 13) I typed my last name in wrong.  Can I UPDATE it?  (Hint: Yes, you can!)

`UPDATE table_name SET col1 = val1, col2 = val2 WHERE condition;`

`UPDATE Users SET ContactName = 'John Jones', Country= 'France' WHERE CustomerID = 32;`

Key point: **Make sure** to put in the `WHERE` condition here, otherwise you'll `UPDATE` every record in your table.  That would be poor.  

### 14) Oh, well if I can UPDATE, I'd also like to DELETE.

Ok then, we can do that.

`DELETE FROM table_name WHERE condition;`

`DELETE FROM Users WHERE UserName='John Jones';`

Key point!  Just like with `UPDATE`, **make sure** to put that `WHERE` clause in there.  Otherwise, you'll `DELETE` the entire table.  And won't you be sad!

### 15) I have three short friends.  Which one is the shortest though?

`SELECT MIN(col_name) FROM table_name WHERE condition;`

`SELECT MIN(Height) AS Shortest FROM Friends;`

This time, `WHERE` is optional.  I could put the names of the 3 friends, but don't need to.

## Head's up, the next 3 are math-y!
### 16) Get a COUNT of records that match a criteria...

`SELECT COUNT(col_name) FROM table_name WHERE condition;`

`SELECT COUNT(ProductID) FROM Products WHERE Price < 200;`

### 17) AVERAGE value of a numeric column.

`SELECT AVG(col_name) FROM table_name WHERE condition;`

`SELECT AVG(Price) FROM Products;`

### 18) SUM the value of a numeric column. 

`SELECT SUM(col_name) FROM table_name WHERE condition;`

`SELECT SUM(Quantity) FROM OrderDetails;`

### 19 & 20) Look, I'm not gonna kid you, LIKE is like a simplified regex for SQL. There's a lot of little options. So it gets 2 numbers on the hit parade.

`LIKE` is used in `WHERE` clauses, to search for specific parameters.
Two symbols are used with `LIKE`
%  === 0, 1 or multiple characters
_    === 1 character

`SELECT col1, col2, ... FROM table_name WHERE colN LIKE pattern;`

`SELECT * FROM Customers WHERE CustomerName LIKE 'a%';`

Put that in and you'll get all customers' names that begin with "A".

OTHER % and _ options...
'&a'  -- any customer name that ends in "A".
'%the%' -- any customer name with "THE" in it anywhere.
'_d%' -- any name that has a d in 2nd position.
'a%e' -- any name that starts with "A" and ends with "E".
'a_%_%' -- any name that starts with "A" and are 3 or more characters long.


Well, phew, we did it!  Well, I wrote it and you read it!
I think I'm gonna need a 3rd installment.  There's a ton of SQL to know.  It really is so important to have good resources on this though and to review.  It's the basis of all databases!  Get hip man!  


