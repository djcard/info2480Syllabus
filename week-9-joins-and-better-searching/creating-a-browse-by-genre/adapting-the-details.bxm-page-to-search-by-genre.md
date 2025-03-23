# Adapting The Details.bxm Page to Search By Genre

The details page itself only need to be slightly tweaked.&#x20;

1. Currently it is searching on the form.searchTerm submission. Let's change that so it searches on searchTerm regardless of whether it comes in on a form or in a link. \
   Add `<bx:param name="searchTerm" default="" />` to the top of the page.\
   \
   Let's also add a param for the genre variable.\
   `<bx:param name="genreId" default=0 />`\
   \
   Why did we make the searchTerm default to "" but the genreId default to 0?
2. The second is to pass the “genre” param to our searchBooks function in bookstore.common.books.

`<bx:set bookinfo = bookstoreFunctions.searchBooks( searchTerm, genreId ) />`

3. In the searchBooks function, we need to change our arguments to accept both a searchTerm and a genre. Don't forget to put in default values of "" and 0 in case they are not passed in.&#x20;
4. We already have a query in there to search based on the “searchTerm” param. We need to add an “if / then” statements so that when we are searching by “searchTerm” it will use one query and another if we are submitting a genre”. While we're at it, let's also adapt our query so that it is a little more secure by using named parameters. These are submitted separately from the main SQL and are examined more closely for issues from bad actors such as SQL injection attacks and so on.&#x20;

```
if(searchTerm.len() != 0) {
     return queryExecute("
        SELECT * from books
        INNER JOIN publishers
        ON books.publisherId=publishers.id
        WHERE title like :searchTerm
        OR isbn13 like :searchTerm",
        { searchTerm: '%#trim(arguments.searchTerm)#%'})
 
} else if( genreId > 0){
    return queryExecute("
        SELECT * from books b
        INNER JOIN genresToBooks gtb
            ON b.isbn13 = gtb.isbn13
        WHERE gtb.genreid=:genreId ",
        {
           genreId:arguments.genreId
        }); 
}
```

Notice how both queries have the book data as well as the name of the publisher so that our “view” code will be able to work regardless of which query is returned. Since our queryToBooks table only allows each combination of book and genre to be entered once, we shouldn't get duplicate records of books.

## Bonus

Can you make it so that you can show the genres to which a book belongs on the OneResults.bxm page? How about clicking on the name of that genre to get other books in the same genre?

Can you make it so that you can click on the publisher's name in the book listing and get books by that publisher?
