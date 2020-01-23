---
title: SQL Primer
author: Addama
excerpt: Introduction to basic SQL queries
permalink: /sql-primer/
---

# SQL Primer

*This is a basic introduction to SQL as a language. If you are already comfortable with SQL, this might be too low level for you!*

SQL, or *Structured Query Language*, is a family of languages informally adhered to by the majority of database systems, and is used to programatically retrieve, add, update, and delete data from the database as well as construct the database in the first place.

Notice that it says *family of languages* above - there is no one SQL, though if you know one flavor of SQL you essentially know them all. For example, Microsoft's Transact SQL (T-SQL) differs from Oracle's MySQL in the functions and filtering capabilities available, as well as how some statements are interpreted. They are otherwise functionally the same, and for most purposes you won't be able to tell them apart.

For the purposes of this document, I will be referring specifically to MySQL.

## How A Database Works

While we won't be getting too far in depth with database architecture, it is important for you to know the basic structure of a database.

A database is a container for *tables*, and tables are containers for data that are constrained to *rows* and *columns*. There's more to it than that, of course, but at this level, that's all you need. If you've ever used a spreadsheet, you are already familiar with how a database works and behaves. In fact, the only thing you're missing is SQL.

![Image of a spreadsheet cells and rows](/images/2019-11-25-SQL-Primer/spreadsheet.PNG?style=center)
![Image of a database cells and rows](/images/2019-11-25-SQL-Primer/database.PNG?style=center)

When making a table, you can link it to other tables by setting a column as a *key*, specifically *primary keys* and *foreign keys*. Primary keys are the important columns in the table - these must be unique, are often used by other tables to refer back to this table, and generally only happen once per table. These are IDs, catalog numbers, serial numbers, etc. Foreign keys are usually primary keys from other tables, but are important to how this table's data makes sense. For example, let's say you have a table for all of your users, and a table for the computers in the office. In order to correlate the two, you could do the following:

* Create a new table with three columns: 
  * `id`, the primary key, which will generally not be used except to refer to a specific row in this table
  * `user_id`, a foreign key which points to the primary key of the users table, which is also called user_id
  * `computer_id`, a foreign key which points to the primary key of the computers table, which is also called computer_id

Now, if you want to know what computer someone is using, you can use this new "*lookup table*" as a bridge between the computers and users tables. If someone tries to put something screwy in there, the database will know to look in the users or computers to verify if the values they're putting in actually match up to the primary keys in those tables.

Unique to databases is the concept of committing and rolling back changes. Hold on - if you've used Git, you're already familiar with committing changes. Any change (i.e. most things aside from SELECT) is done temporarily, and must be committed in order for them to take effect for real. If your changes turn out to be harmful or not what you want, you can simply roll them back and it will be like they never happened.

There is a fairly important topic to databases that won't affect you directly, but it would be good for you to know and keep in mind. *Normalization* is the process and idea that data should be segmented and kept separate at the lowest level possible. In our lookup table example above, we satisfy normalization by keeping the relationship between users and computers in its own table rather than trying to shoehorn it into one or both of the pre-existing tables. This allows the relationships and even just the existence of data to be more easily managed and kept track of. A perfectly normalized database (subject to debate on what "perfect" means) will have all discrete *kinds* of data and each discrete relationship between it all given its own table. 

Databases are pure data that has been organized and put away neatly. That's great for data, but not useful for humans and how we think. To pull the data out and use it in a way that's useful to us, we need to talk to the database and tell it what we want. We use SQL for this.

## Language Basics

At this introductory level of SQL, we can break the language up into 4 distinct kinds of *statements* that are used to build *queries*:

* **SELECT:** get data from the database
* **UPDATE:** change data in the database
* **INSERT:** add data to the database
* **DELETE:** remove data from the database

There are other statements for creating and updating entire databases, tables, schemas, and much more; for now, these will do. 

Each of these statements performs a single function, and there is little to no crossover between them. In more advanced queries, you might see a SELECT being used inside another statement to be more specific about what rows you want to affect. 

It is convention to write SQL statements in all caps, and the data (column names, etc) matching the case they appear as inside the database. SQL statements themselves are not case sensitive, however. In most implementations, these two queries will perform exactly the same:

* `select user_id from users;`
* `SELECT user_id FROM users;`

As you can see, individual queries end with a semicolon. This isn't as important when you're running one query at a time, but when you have multiple queries to run, these help the database know when one command ends and one begins. I would suggest getting into the habit of using semicolons so you don't get confusing error messages later on.

SQL statements will always follow a predictable format and order. One SELECT statement will be written in the same order (more or less) as another. The only difference tends to be whether you include various optional *clauses*.

Let's look at a few example queries so we can get an idea of what that means in practice.

1. `SELECT * FROM users;`
1. `SELECT * FROM users WHERE user_id = 1;`
1. `SELECT user_id, name FROM users;`
1. `SELECT user_id, name FROM users WHERE user_id = 1;`

Can you read those and get a general feeling for what they're doing? I bet you can - SQL is a fairly simple language to read and write.

In queries 1 and 2, we are SELECTing `*`, which means "everything" from the users table. In queries 3 and 4, we are instead specifying which columns we want to see. Only these columns will be returned in the result. In queries 2 and 4, we filter the results to only the rows in which the `user_id` column has a value of 1 by using a WHERE clause. In all cases, notice how they are written exactly the same, in exactly the same, predictable order. Not too bad!

## The SELECT Statement

![Complete specification of a SELECT statement in MySQL](/images/2019-11-25-SQL-Primer/select.PNG?style=center)

The SELECT statement is the most basic tool at your disposal, allowing you to get data from the database in a way that you want to get it. There are a lot of options for how that data is retrieved, formatted, compared, and displayed.

SELECTs follow this general pattern: **SELECT** *columns* **FROM** *tables* **WHERE** *columns are like this* **ORDER BY** *columns*. 

There were several examples of a SELECT in the last section, but let's look at something a little more complicated. This refers to the user and computer lookup table introduced above.

```sql
SELECT
  users.name AS 'Name',
  users.title AS 'Title',
  computers.name AS 'Computer',
  computers.location AS 'Location'
FROM 
  users_computers,
  users, 
  computers
WHERE
  users_computers.user_id = users.user_id
  AND users_computers.computer_id = computers.computer_id 
  AND users.fired = 'N'
  AND computers.needsUpdate = 'Y'
ORDER BY
  users.name,
  computers.name
LIMIT 10;
```

Wow, that's quite a bit longer, but we can learn a lot from the differences here. Notice how the command has been spaced out a bit? This is only so that we can read it better - once the database recieves it, all of that formatting will be ignored. Second, you no doubt saw that we're pulling from multiple tables. In this example, we're using the lookup table given a few sections above as a bridge between the `users` and `computers` tables. To do this, we need to correlate the three tables together by establishing that the values in their columns are linked. Once we establish that fact, all three tables can be queried and broken apart like they're one big data set.

In order to get exactly what we're asking for, we are prepending the table name to the column names so that the database knows *which* `name` column we're talking about - if we didn't specify, it wouldn't know and would have to guess! The exception to this is if you know for a fact that only one table has a column with that name.

So what does this even do? If you break it up into parts, this is what it looks like:

1. **SELECT users.name as 'Name', users.title as 'Title', computers.name as 'Computer', computers.location as 'Location'**
  * Show me the name and title columns from the users table and the name and location columns from the computers table
  * Additionally, when you show me those columns, call them "Name", "Title", "Computer", and "Location" instead of their column names (the default) which would be the less-readable "name", "title", "name", and "location"
1. **from users_computers, users, computers**
  * These are the tables I will be using/referring to for this operation. Notice how we are referring to users_computers but never SELECTing any of its columns - this is okay!
1. **where**
  * I want you to filter the data before you give it back to me
1. **users_computers.user_id = users.user_id and users_computers.computer_id = computers.computer_id**
  * Show me only user_ids and computer_ids that have rows in the users_computers table. This will prevent the query from showing computers that have no users and users that have no computers
1. **and users.fired = 'N'**
  * For my purposes, I don't care about users who aren't here anymore, and would therefore have their fired column set to 'Y'
1. **and computers.needsUpdate = 'Y'**
  * Show me only computers that are marked as needing an update
1. **order by users.name, computers.name**
  * Order the rows alphabetically by the name column in the users table, then by the name column in the computers table
1. **limit 10**
  * Only show me the first 10 rows, because I don't have time to look at all of them right now
  
Based on all of that, we can now see that we will receive a tabular report of all computers that need an update, the name of the computer and where it is, as well as the name and title of the user that computer belongs to. The report will be ordered by user name, then by computer name. The final result might look something like this:

```
+-----------------+-------------------+-------------------------+----------+
| Name            | Title             | Computer                | Location |
+-----------------+-------------------+-------------------------+----------+
| Andrews, Adam   | Financial Planner | PBQ1223141tj2p3t23-2352 | Annex B  |
| Andrews, Alice  | Analyst           | PBQ1223141tj2p3t23-2353 | Room 14  |
| Bravo, Billy    | CEO               | ARJ1435920359-23424-12Q | Room 32B |
+-----------------+-------------------+-------------------------+----------+
```

SELECTs can also be used as *subqueries*, for those times when you don't know exactly what data or columns you need for some other statement, but know where to get it in the database. That can look like this:

```sql
SELECT
  name
FROM
  computers
WHERE
  computer_id IN (
	SELECT 
	  computer_id 
	FROM 
	  users_computers,
	  users
	WHERE
	  users_computers.user_id = users.user_id 
	  AND users.fired = 'Y'			
  );
```

In this example, we want a list of computer names, where only computers belonging to fired employees are shown. We don't know which employees those are ahead of time, and even if we did, it would be a pain to write those user_ids out as a list every time we needed to run this query. Rely on the database to pull out and format its own data whenever you can.

## The UPDATE Statement

![Complete specification of an UPDATE statement in MySQL](/images/2019-11-25-SQL-Primer/update.PNG?style=center)

UPDATEs are exactly what they sound like. Some datapoint in the database needs to be changed. Note that this is not changing the structure of the table, the columns, etc - only an individual datapoint in a specific column and/or specific row(s). 

UPDATE statements generally follow this pattern: **UPDATE** *tables* **SET** *columns equal to their new values* **WHERE** *columns look like this*. It's not as easy to explain like this than a `SELECT`, so let's look at some examples.

* `UPDATE users SET title = 'Financial Analyst' WHERE title = 'Financial Planner';`
* `UPDATE users_computers SET user_id = 42 WHERE computer_id = 69420;`
* `UPDATE computers SET location = 'Annex B', needsUpdate = 'Y' WHERE location = 'Room 14';`
* `UPDATE users, computers SET dateMoved = '2019-01-01', location = 'Annex B' WHERE location = 'Room 14';`

So overall, not that complicated except maybe for that last one. You *can* update more than one table's data at a time, and the update will apply to all data points on all tables you specify that match the specifications in the WHERE clause. Until you have a reason to, however, stick with changing as little as possible with each query.

## The INSERT Statement

![Complete specification of a INSERT statement in MySQL](/images/2019-11-25-SQL-Primer/insert.PNG?style=center)

The INSERT statement is used to add rows to a table. Using it requires some foreknowledge of the table's columns because you have to specify the columns you want to add data into.

INSERT statements follow one of these two patterns: 

* **INSERT INTO** *table* **(***list of columns***)** **VALUES** **(***list of values***)**
* **INSERT INTO** *table* **SET** *columns equal to their values*

Though functionally the same, each one has some benefits and drawbacks. Here is the same query expressed both ways:

**INSERT INTO ... VALUES**
```sql
INSERT INTO users (name, location, fired) VALUES ('Bravo, Billy', 'Room 32B', 'N');
```

**INSERT INTO ... SET**
```sql
INSERT INTO
  users
SET
  name = 'Bravo, Billy',
  location = 'Room 32B',
  fired = 'N';
```

As you can see, the *INSERT INTO... SET* variation is a little easier to read, and doesn't require you to split the column names and values apart. On the other hand, the *INSERT INTO... VALUES* variation is better when you are pulling the list of columns or values from the database or some other data source. That makes writing programmatical queries easier with less pre-formatting than would be required in the second example.

## The DELETE Statement

![Complete specification of a DELETE statement in MySQL](/images/2019-11-25-SQL-Primer/delete.PNG?style=center)

The DELETE statement is essentially the opposite of the INSERT statement. Using it, you can remove one or more rows from one or more tables.

The DELETE statement follows this pattern: **DELETE FROM** *tables* **WHERE** *columns are like this*

Be aware when removing rows - once done, that data is gone! Double and triple check your queries (not just DELETEs, but any query) to be sure it will do exactly what you want and not have any side effects. 

Here is an example of a DELETE statement:

```sql
DELETE FROM users WHERE fired = 'Y';
```

You can also delete from multiple tables at once, though this is generally more complicated and would be better left until you are more comfortable. Below is an example:

```sql
DELETE FROM
  users,
  users_computers
WHERE
  users.user_id = users_computers.user_id
  AND users.fired = 'Y'
```

## Functions

Like any other high level computer language, SQL has built-in functions to make your job easier and perform tasks you wouldn't otherwise be able to. 

I have outlined a few useful/common ones below, but there are quite a deal more, some of which do very specific things like parsing JSON or generating unique ID strings.

### COUNT()

The COUNT function counts the number of non-null rows based on the column you specify (or `*`). If you are selecting more than one column, you will usually have to supply a GROUP BY clause to specify which column is the one being counted.

```sql
SELECT
  users.name AS 'Employee',
  COUNT(*) AS 'Computers Assigned'
FROM
  users,
  users_computers
WHERE
  users.user_id = users_computers.user_id
GROUP BY
  users.name;
```

```
+--------------------+--------------------+
| Employee           | Computers Assigned |
+--------------------+--------------------+
| Bravo, Billy       | 2                  |
| Borchester, Graham | 1                  |
| Cardenas, Roger    | 1                  |
+--------------------+--------------------+
```

If you need to sort the results by a COUNT column, you need to supply its entire name in the ORDER BY clause, like below:

```sql
SELECT 
	COUNT(user_id) AS 'Number of Users'
FROM
	user
ORDER BY
	COUNT(user_id)
```

### CONCAT()

The CONCAT function concatenates (joins) two or more values together into one string.

```sql
SELECT
  CONCAT(firstName, ' ', lastName) as 'Name'
FROM
  users;
```

```
+--------------------+
| Name               |
+--------------------+
| Billy Bravo        |
| Graham Borchester  |
| Roger Cardenas     |
+--------------------+
```
### UPPER()/LOWER()

The UPPER and LOWER functions change the case of text data to upper case or lower case respectively. This can be useful for comparing strings where you're not sure what the case will be.

```sql
SELECT
  UPPER(name) as 'UPPER',
  LOWER(name) as 'LOWER'
FROM
  users;
```

```
+--------------------+--------------------+
| UPPER              | LOWER              |
+--------------------+--------------------+
| BRAVO, BILLY       | bravo, billy       |
| BORCHESTER, GRAHAM | borchester, graham |
| CARDENAS, ROGER    | cardenas, roger    |
+--------------------+--------------------+
```

### LIKE/NOT LIKE

LIKE and NOT LIKE are actually operators (like = or +) rather than functions, but it's easier to group them here.

LIKE and NOT LIKE are used to match data where you're not sure exactly what you're looking for, or you *do* know, but it would be easier to look for it based on a pattern. By default, you can use the `%` symbol as a wildcard, standing in the place of characters you don't know or don't care about.

```sql
SELECT
  name AS 'Computer',
  computer_id AS 'ID'
FROM
  computers
WHERE
  computer_id LIKE 'PDQ%'
  AND computer_ID NOT LIKE '%_v1';
```

```
+------------------+------------------------+
| Computer         | ID                     |
+------------------+------------------------+
| HP COMPAQ 2100   | PDQth240ha34p98ah34_v2 |
| HP COMPAQ 2100   | PDQ305h0f239u203t92_v3 |
| DELL 2600 SE MAX | PDQrrh203f8f32hf239_v2 |
+------------------+------------------------+
```

### DESCRIBE

DESCRIBE is a statement similar to SELECT, in that you are asking the database for information. The difference is, DESCRIBE will return information about a table, such as its columns, and what data type those columns expect.

DESCRIBE is a more friendly alias for `SHOW COLUMNS FROM ...`, and is very similar to the EXPLAIN statement.

```sql
DESCRIBE users;
```

```
+-----------+-----------+------+-----+---------+----------------+
| Field     | Type      | Null | Key | Default | Extra          |
+-----------+-----------+------+-----+---------+----------------+
| user_id   | int(9)    | N    | Y   |         | auto_increment |
| firstName | char(50)  | N    | N   |         |                |
| lastName  | char(50)  | N    | N   |         |                |
| name      | char(125) | Y    | N   |         |                |
| location  | char(200) | Y    | N   |         |                |
| fired     | char(1)   | Y    | N   | N       |                |
+-----------+-----------+------+-----+---------+----------------+
```

### NOW()/CURDATE()/CURTIME()

Dates in SQL have a whole swathe of functions dedicated to them, but the three you will likely need or run into are NOW, CURDATE, and CURTIME. 

* **CURTIME** returns the time in `hh:mm:ss` format, based on when the function is called
* **CURDATE** returns the date in `YYY-MM-DD` format, based on when the function is called
* **NOW** returns both the date and the time in `YYYY-MM-DD hh:mm:ss` format, but the datetime it returns is based on when the query was started

You can see in the example below, NOW doesn't change, because it's based on when the script started, but SYSDATE (which is similar to NOW, but specific to the server's time settings rather than the database's) gives the present datetime each time it's called.

![Example of NOW and SYSDATE returning datetimes](/images/2019-11-25-SQL-Primer/date.PNG?style=center)

# Exercises

What good is all of this knowledge if you can't put it into practice? Ideally you would find a database that means something to you and play around in there; I can't know what database that is or what tables it has, though, so that makes writing exercises difficult. That being the case, I will assume that you have access to a Summit database for the Baker Clinic with at least schema 106 - preferrably one that is for testing so that nothing you do will mess anything up in production.

You can do these in the console or with a tool like DBeaver.

**Easy**
1. *Describe* the user table
1. Get everything from the user table
1. Get everything from the user table but order the rows by the privilege column
1. Get everything from the user table row for the 'Xtract Admin' user
1. Get only the displayname, password, and deleted columns for the user table row for the 'Xtract Admin' user
1. Using the query above, give each column a new, more readable name

**Medium**
1. Add a new location in the location table
  * *The location_id column will fill itself out, so don't give that one a value!* You can tell this is true by DESCRIBEing the table and seeing that it has `auto_increment` in the Extra column of the DESCRIBE
1. Update the name of the location you just created to something new
1. Delete the location table row you just added
  * *Be very sure you're pointing at the correct row!*
1. Get user.displayname and user_group.name from the user and user_group tables, using the user_group_user *lookup table* as a bridge
  * Give each column a new name so the output makes more sense

**Hard**
1. Get all of the rows from the config table whose names end with '3'
1. Get all of the rows from the config table whose names contain 'hot'
1. Get all of the rows from the config table whose names end with '3', but do not contain 'bottle'
1. Get all of the rows from the config table whose names start with 'bottle' **or** end with '3'
1. Get a count of the number of users within each user group
1. Get a count of the number of prescriptions that each user has created, ordered from **most to least** then by user displayname **alphabetically**, limited to 3 rows
  * *You might need to do some research to figure this one out!*

**Crazy**
1. Get only the primary and foreign key columns (except for Provider Config), the prescription priority, and the patient DOB for all rows from the prescription table, but replace all of the foreign keys with appropriate, human-readable values (usually name, displayname, or the first and last names joined together) that those foreign keys are pointing to. Give each column a new name. Sort the output alphabetically by Clinic, then alphabetically by Provider, then by Priority from most to least, then by Patient reverse alphabetically. Place the columns in that order in the output, with the remaining columns arranged alphabetically after.

[Answer Key](/images/2019-11-25-SQL-Primer/sql_answer_key.txt)

# Glossary

* **Statement**
  * The individual operations you want to perform on the database, expressed as a command like SELECT or UPDATE
* **Query**
  * One or more statements fully realized and able to be executed by the database. If statements are words, queries are full sentences
* **Table**
  * A table is essentially a collection of columns and rows that are used to store related data. The columns each store a different kind of data, and could be anything from a name, an ID, a true/false boolean, etc
  * Tables are similar conceptually to an individual sheet in a spreadsheet application
* **Database**
  * A database is a collection of tables, plus an engine that can interpret SQL queries, and a whole bunch of extra metadata that describe how those tables and the data in them should act and be accessed
  * A database is similar conceptually to a collection of sheets in a spreadsheet application

# Resources

* [MySQL Statements Reference](https://dev.mysql.com/doc/refman/8.0/en/sql-statements.html)
* [MySQL String Functions Reference](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html)
* [MySQL Number Functions Reference](https://dev.mysql.com/doc/refman/8.0/en/numeric-functions.html)
* [MySQL Date Functions Reference](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html)
* [More in-depth query tutorial](https://dev.mysql.com/doc/refman/8.0/en/entering-queries.html)
* [Common query examples](https://dev.mysql.com/doc/refman/8.0/en/examples.html)
