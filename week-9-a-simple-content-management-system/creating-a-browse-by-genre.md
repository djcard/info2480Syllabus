# Creating a Browse by Genre

## Background

We have added a search function to our site but obviously we don’t have every book in existence in our site. In fact, we have very few although what we’ve built could accommodate quite a lot. Typically, people search for a book they have heard of or a topic in which they are interested. Categorizing books according to topic or genres allow the user to look for information (or books) by browsing instead of guessing what keywords are going to get them what they want. It’s a different approach that allows users to find their content in the manner they choose.

In this exercise, we are going to add to our existing site the ability to browse by genres. This includes a few parts and is contingent on a few different techniques which we have not investigated yet. These are listed below.

* In a form, if multiple inputs have the same name, they are submitted together and are separated by a comma like this: item1,item2,item3,item4 etc. BoxLang has built in support for handling lists like this. We can use \<bx:loop list=””> to loop over the list and do something with the individual items.
* We are going to use a feature in JavaScript which allows up to check a checkbox in a form based on its Id. This is document.getElementById(‘id’).checked=true;
* We are use a new SQL technique which includes the word DISTINCT. This means, of all the rows in the datatable, give me each value only once. If there are 1000 rows and they all have the same value, let’s say “bob”, only one row with “bob” in it will be returned. If there are 500 “bob”s and 500 “steve”s, then two rows will be returned which will be bob and steve. Make sense?
* The use of a “many to many” join by using a separate table to link the genres to the books. Our publishers are linked to book by a one-to-many. This means that each book has one and only one publisher. For genres, each book can have many genres and each genre can be assigned to many books. This is many to many. The best way to handle that relationship is to have a table which contains the index from each of the tables and links them together.



###

###

###
