# Adapting The Details.bxm Page to Search By Genre

The details page itself only need to be slightly tweaked. Currently it is searching on the form.searchTerm submission. Let's change that to&#x20;

The second is to pass the “genre” param to our bookDetails query in bookFunctions.cfc.

`<cfset bookinfo = bookstoreFunctions.bookDetails( searchme, genre ) />`

Currently, we already have a query in there to search based on the “searchme” param. We need to add an “if / then” statements so that when we are searching by “searchme” it will use one query and another if we are submitting a genre”

```
if(searchme.len() != 0) {
    var qs = new query(datasource = application.dsource);
    qs.setSql("
        SELECT * from books
        INNER JOIN publishers
        ON books.publisher=publishers.id
        WHERE title like :searchme
        OR isbn13 like :searchme ");
    qs.addParam(name = "searchme", value = '%#trim(arguments.searchme)#%');
    return qs.execute().getResult();
} else if( genre.len() != 0){
    var qs = new query(datasource = application.dsource);
    qs.setSql("
        SELECT * from books
        INNER JOIN genreToBook
            ON books.isbn13 = genreToBook.isbn13
        INNER JOIN publishers
            ON books.publisher=publishers.id
        WHERE genreid=:genre ");
    qs.addParam(name = "genre", value = trim(arguments.genre));
    return qs.execute().getResult();
}
```

Notice how both queries have the book data as well as the name of the publisher so that our “view” code will be able to work regardless of which query is returned.

## The Label

When we have multiple results we might want to display a label showing what we used to get those results. In our manyResults function on details.cfm, add a header over the results like this:

```
<div>
    <h3>
        <cfoutput>
            #bookstoreFunctions.resultsHeader(searchme, genre)#
        </cfoutput>
    </h3>
</div>
```

Make a function in bookstore.cfc called resultsHeader and have it return something like “Keyword: idghdfghdfhdf” or “Genre: Mystery” depending on what was submitted.

Make sense? Look at the sample as well as the code listed at [https://comweb.uml.edu/CodeBase/](https://comweb.uml.edu/CodeBase/) for week 9 and see how it all works together.
