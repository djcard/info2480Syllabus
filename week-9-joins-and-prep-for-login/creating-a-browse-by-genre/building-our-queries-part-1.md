---
description: All of the methods below will go into the bookstore.common.books class
---

# Building our Queries: Part 1

## allGenres()

This function will return all the genres in out genres table. By now you should have all the knowledge you need to create this query. If you need to go back and look at the other queries we've developed, go for it.&#x20;



## saveGenreToBook()

This will accept two arguments (data passed into the function) which are the id of a genre and the isbn13 of a book and then insert that data into the `genresToBooks` table. By now you should have all the knowledge you need to create this query. If you need to go back and look at the other queries we've developed, go for it.&#x20;



## clearAllBookGenres()

This will accept the isbn13 of a book and then delete the records in the `genresToBooks` table for that isbn13. This is the first query we've written that involves delete but it is not very different from the other queries that we've written. It is VERY important that you include your WHERE clauses in a delete function. Otherwise you can delete all the records in your database.

`delete from genresToBooks where isbn13=''`



## allGenresForBook()

This query is a little more complicated and it will be easier to visualize if we already have data in our table so we will revisit it later. For now simply create the function and have it accept and genreId with the default value of 0 and an isbn with the default value of  an empty string

`function allGenresForBook(genreId=0, isbn13=''){`\
\
`}`

