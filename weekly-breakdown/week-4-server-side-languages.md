# Week 4: Server Side Languages

What is a server language?

What is a scripting server?

Syntax (Tag vs Script)

Variables, formatting vs value

### Background

Structured Query Language (SQL – pronounced see-kwell) is the language of relational databases. It is the language understood by the majority of databases in the world and can be found in many applications whether they are in used on the web, in a desktop application or on mobile devices. The SQL language is the generic umbrella for the language that is common among all databases. Like with everything in technology, there are variants within the SQL world. Some of these are listed below:

* T-SQL – an extension of SQL developed by Microsoft to be used in MSSQL
* PL/SQL – an extension of SQL developed by Oracle
* PL/pgSQL – an extension of SQL developed by PostgreSQL

The core part of the language is the same in all of these. The parts that are unique are meant to be used on that particular database for improved functionality. For our purposes, we are going to stay within the common SQL language and not stray into the edge cases.

## What Can You Do With Data

Before we get into the actual language, let’s think about what you can do with data. We’ve already seen how the data in a relational database is set up in columns (fields) and rows (records). What can you do with these rows and records?

* You can put new data in
* You can extract data
* You can change the data
* You can delete data
* You can add more columns to the table
* You can edit the column in the table (change the name, datatype or size)
* You can delete a column from the table

That’s about it unless you can think of any more. Can you?

SQL has a set of **Key Words** which make up the majority of the language. Having a mastery of these key words will go a long way to giving you a strong foundation for using SQL in your applications and web sites.

Let’s go through these actions one by one.

## Putting New Data Into A Data Table

Before we can get data out of a table, we need to put data into the table. This is done using the INSERT keyword. A simple insert statement looks like this:

INSERT INTO books (title, year, pages) VALUES (‘The Wind In The Willows’,1908,272)

Let’s break that down.

**INSERT**  - the keyword for putting data into a data table

**INTO** – The keyword signifying the name of the table to which the data is being put is next.

books  - The table into which the data is being put

(title, year, pages) – The list of fields which are receiving data

**VALUES** – The keyword signifying that the values are next

(‘The Wind In The Willows’,1908,272) - The list of values which are being inserted. These need to line up exactly with the list of fields above. If you need a place holder for an empty value use ‘’ like this: (title, year,pages) values (‘The Wind In The Willows’,’’,272).

Notice how the strings have single quotes around them and the numbers do not. It’s important to use single quotes because double quotes have their own significance. Any idea how you would insert a word that was a contraction like this: (title, year, pages) values (‘It is, Isn’t it’,2014,54)? That, as written will throw an error. Why? How do you fix it? Tell you what, put a pin in that. We’ll come back to it.

## Extracting Data

The most basic and commonly used action to a database is to find a dataset. A dataset is simply a collection of information. Often this data is filtered to find only the data that meets certain criteria. The keyword to perform this action is SELECT.

The most basic SQL statement looks like this:

**SELECT** \* **FROM** _books_

The capitalization is optional. This statement will retrieve all the records from a data table called “books.” Let’s break it apart

**SELECT** – this is the key work that says we are going to create a dataset based on data from this database.

*
  * This is shorthand for “every field in the data table”

**FROM** – this is the key word that tells the server that the table from where we want the information is next.

Books – the name of the table.

As is, this statement will extract every record of every field from the database. In short, the entire thing. We might not want that so let’s look how we can filter the data we get back from our request. There are two ways to filter the data

1. Asking specifically for certain fields rather than asking for all of them by using \*
2. Putting conditions on the records which are returned.

Here is what that looks like:

**SELECT** title,year,isbn **FROM** books **WHERE** title=”The Wind In The Willows”

The breakdown:

**SELECT** – this is the key word that says we are going to create a dataset based on data from this database.

title,year,isbn – The list of fields we want from the data table

**FROM** – this is the key word that tells the server that the table from where we want the information is next

books – the name of the table.

**WHERE** – the keyword saying that this is the start of the criteria

title=”Gone With the Wind” – The field and value we want.

In regular English this statement says “Give me the title, year and isbn from the BOOKS table for all the books with the title, “The Wind In The Willows”.

## A Closer Look At Criteria

In the previous section we saw how we can use criteria to filter the data coming from a database. However, we looked at one instance with one table and one value. Can we filter on more than one field? Yes. By using the AND and the OR keywords and a few OPERATORS, we can string together a list of criteria. Here are a few examples:

**Two values for the same field**: WHERE title=’The Wind In The Willows’ OR title=’It Happened One Night’

**Two Fields**: WHERE year=2015 and publisher=’Sony’ (notice the lack of quotes around the 2015. This means it’s a number. All of the other values which are string have quotes around them. )

**A Range**: WHERE year >=2000 and year <=2015

Other Operators

> greater than

> \= greater than or equal to

< less than

<= less than or equal to

<>  greater than or less than (or simply “not equal to” or “is not”)

!= Not equal to

We can also search using with what is called a wildcard. A wildcard is a symbol that substitutes for the unknown. Let’s say we want to find a book but we don’t remember what it is called. We can use the keyword “LIKE” and a wildcard. The wildcard symbol in SQL is “%” – the percent sign. Here is how it is used:

SELECT \* from books WHERE title LIKE ‘T%’

This gives me all of the books where the title starts with “T”. The position of the wildcard is important. In this example, “T” is the first letter so any of the results have to start with “T”. If we wanted to find any books that end in “willows”, it looks like this:

SELECT \* FROM books WHERE title like ‘%willows’

This will find any books in our database where the letters “willows” are the last characters in the title. If there is a space after “willows” it will not find it since we didn’t tell it to find a book where willows was in the title someplace, we said where it was at the very end of the field. How would you write a query that said to find a title where willows was in the title someplace?

SELECT \* FROM books where title like ‘%willows%’

In that case we can use the wildcard multiple times. If we know that the title starts with a T and has “willows” in it, we would type:

SELECT \* FROM books where title like ‘T%willows%’

This can be handy because sometimes extra characters such as spaces, tabs, line feeds or carriage returns can be inserted in the db at the end of a value. The LIKE keyword is very powerful. However, it can also take a long time for these queries to run since it needs to read the entire field and look for patterns in every row of the database and that can take time so it makes sense to think through how you write your queries.

Quick Note: I find that when querying using dates, it is best to use a 4-digit year - two-digit month - two-digit day and. (i.e. ‘2015-05-14’).

## Updating Data

Next up is editing data already in the database. Here is a sample:

**UPDATE** books **SET** title=’More Windy and More WIllowy’;

By now, that should be almost readable:

**UPDATE** – The key word for editing a row or rows in the datatable

books – The table with the data being edited (you can usually only do one table at a time)

**SET** – the keyword signifying that the new fields and values are next

title=’More Windy and More Willowy’ – the field followed by the new value.

HOWEVER, as written, that SQL statement will update every single row in the data table with the new title which is, typically, not what we want. So once again we employ the criteria we studied above. We are also starting to delve into the reason why we need at least one field that makes each row unique. We use that unique value as the criteria to update only the row we want.

UPDATE books SET title=’More Windy and More Willowy’ WHERE title=’The Wind In The Willows’;

We can do as many field as we choose like this:

UPDATE books SET title=’More Windy and More Willowy’, year=1908, pages=272 WHERE title=’The Wind In The Willows’;

We string the fields and values together using a comma (,) as the separator. If a field is not listed in the update list, its value in the data table is not changed.

Make sense?

## Deleting Data

This can be a nerve-racking process because it is possible to delete every record from a data table with three words:

DELETE FROM books;

That will delete every single row in the books table. The potential to do a lot of damage is so great that quite often the ability to delete data is turned off at the server level. Instead, often, rather than delete the data, there is a special field added to the data model which acts as an “active/inactive” or a “status” field and that is used as part of the criteria. For example, instead of deleting a book that the store is no longer carrying, they might simply set the “available” field to 0. Then the search for a book for sale that starts with “T” would be:

**SELECT** \* **FROM** books **WHERE** title like ‘%T’ and available=1;

If you are going to use the delete statement, I usually write a select statement first to get the exact dataset you want to delete and then use that criteria in the delete statement.

SELECT \* FROM books WHERE title=’More Windy and More Willowy’

then becomes

DELETE FROM books WHERE title=’More Windy and More Willowy’;

This will remove the book with the title of “More Windy and More Willowy” from the books table.

## Sorting The Results

When you run a query, the results are typically sorted in order by the primary key. That means in our bookstore, that the results will be sorted by the ISBN13. That might be good sometimes but in others we might want to sort by another field. The keywords here are **ORDER BY** and **ASC/DESC**. For example:

SELECT \* FROM books where year=2001 ORDER BY title ASC

In plain English this means, “Find everything in the books table that was published in 2001 and give the results to me alphabetized by title in A-Z (ascending) order. If the field is defined as a number, it will be in numerical order. If the field is defined as a date, it will be in chronological order. DESC means descending or Z-A order. You can also sort on multiple fields by putting them together in a list separated by a comma. For example,

SELECT \* FROM books where year=2001 ORDER BY author, year, title ASC

will sort the books, first by author, then by year, then all the titles of the books that came out that year (if there is more than one).

## Conclusion

There is much more to SQL but this is enough to get us started for now. Last week we looked at other SQL code that would create and alter tables. As with every other language, no one memorizes every syntax of the entire language. Instead, learn the basics, and know where you can reference the rest. If you use the syntax enough, you’ll learn the fine points by doing.

**Exercise**: Go to the page [https://comweb.uml.edu/courseItems/sqltest.cfm](https://comweb.uml.edu/courseItems/sqltest.cfm). Follow the directions on that page. There are 9 statements in normal language listed. Translate them into SQL syntax and submit them by typing the SQL into the text area and pressing “Enter SQL”.

A correct answer will add a word or multiple words into the div with the label “Final Answer”. Go in order. The answer will be a 100% readable sentence. When you have completed the assignment, go to Blackboard, take the SQL Query Test and paste your 100% readable sentence in the space provided.
