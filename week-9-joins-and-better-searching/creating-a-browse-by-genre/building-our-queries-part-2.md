# Building our Queries: Part 2

By this time you should have the genres saving to your database. However there are two things missing

1. When we are editing a book, we can not see whatt genres have been assigned to a book
2. We have not adapted our public bookstore to search based on the genres.&#x20;

To do both of these we need to revisit our allGenresForBook function in bookstore.common.books. We want to be able to search any book which has a particular genre (Show me all the books in "Mystery") and also to what genres a book as been assigned ( i.e. what genre is "The Mystery of the Pink Crayfish"? ).&#x20;

To get all the data we need our query is going to be a little more complicated then our others for two reasons.&#x20;

1. It has multiple joins to get data out of three tables (books, genresToBooks and genres)
2. It is going to have dynamic criteria which are only used in certain situations.&#x20;

As a result we are going to build our query little by little as a string and then submit that string as out query. A quick note: we are going to be building our SQL ourselves with code we trust so it is ok to submit the string. You never want to accept sql from some outside source and run it directly on your database. Bad actors can use such a method to run SQL which can harm your site or a your data. Only use inputs you trust.&#x20;

Inside our allGenresForBook function, let start with querying our books table using the submitted isbn13. We'll store the SQL in a string for now.&#x20;

`var ourSQL = "select * from books"` <— This will give us all the data in our books table\
\
Now let's add the first join to the gneresToBooks table. \
`var ourSQL = "select * from books b inner join genresToBooks gtb on b.isbn13 = gtb.isbn13"` \
\
In plan language, this says "give me all the data in the books table and the corresponding data in the genresToBooks table where the isbn13 in the books table is equal to the isbn13 in the genresToBooks table. This raises the question "What are the 'b' and the 'gtb' in our SQL?".&#x20;

Sql statements can get long and when statements get long, they get hard to read and therefore, hard to debug and more prone to mistakes. One way to keep statements shorter is to alias the table. In this case, we are telling SQL server that the books table will be references as 'b' from now on and the genresToBooks table will be reference as 'gtb'. This goes a long way to getting rid of extra text.&#x20;

In our query, we now have the ids for the genres we want to use but not their names. To get those, we need to join one more time to the genres table.&#x20;

`var ourSQL = "select * from books b` \
&#x20;     `inner join genresToBooks gtb on b.isbn13 = gtb.isbn13`\
&#x20;     `inner join genres g on gtb.genreId = g.id"` \
\
Good. This will return all of the books and the genres to which they have been assigned. Some of you might be asking if we needed to query the books table at all in this situation when we could just query the genresToBooks table using the isbn13. The answer is yes. Technically, in this situation, especially given how we're going to use the data, joining to the books table is not strictly necessary but was included here to demonstrate multiple joins.

Now we need to create the conditions. We want to search on the isbn13 when that is submitted and then genre when that is submitted. Remember that we set up a default value of 0 for the genreId and '' for the isbn13.\
`var ourSQL = "select * from books b` \
&#x20;     `inner join genresToBooks gtb on b.isbn13 = gtb.isbn13`\
&#x20;     `inner join genres g on gtb.genreId = g.id";`\
&#x20;     `if(arguments.genreId > 0){`\
&#x20;        `ourSQL = OurSQL & " where gtb.genreId = #arguments.genreId#";`\
&#x20;     `}`\
&#x20;     `if(arguments.isbn13.len() > 0){`\
&#x20;        `ourSQL = OurSQL & " where gtb.isbn13 = '#arguments.isbn13#'";`\
&#x20;     `}`

When the genreId is greater than 0 ( i.e. it was passed in) we then query the genreId based on that submission. When the ISBN13 has a length greater than 0 (i.e. it was passed in) we then query based on that submission. This is based on the idea that we will be either be sending in a genreId or an isbn13. If a query submitted both, it would, at most, return 1 row which would not really be useful.

Now we need to finish that off by running the SQL and returning the results

return queryExecute(ourSQL);<br>
