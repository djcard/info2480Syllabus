# Creating a Browse by Genre

## Background

We have added a search function to our site but obviously we don’t have every book in existence in our site. In fact, we have very few although what we’ve built could accommodate quite a lot. Typically, people search for a book they have heard of or a topic in which they are interested. Categorizing books according to topic or genres allow the user to look for information (or books) by browsing instead of guessing what keywords are going to get them what they want. It’s a different approach that allows users to find their content in the manner they choose.

In this exercise, we are going to add to our existing site the ability to browse by genres. This includes a few parts and is contingent on a few different techniques which we have not investigated yet. These are listed below.

* In a form, if multiple inputs have the same name, they are submitted together and are separated by a comma like this: item1,item2,item3,item4 etc. ColdFusion has built in support for handling lists like this. We can use \<cfloop list=””> to loop over the list and do something with the individual items.
* We are going to use a feature in JavaScript which allows up to check a checkbox in a form based on its Id. This is document.getElementById(‘id’).checked=true;
* We are use a new SQL technique which includes the word DISTINCT. This means, of all the rows in the datatable, give me each value only once. If there are 1000 rows and they all have the same value, let’s say “bob”, only one row with “bob” in it will be returned. If there are 500 “bob”s and 500 “steve”s, then two rows will be returned which will be bob and steve. Make sense?
* The use of a “many to many” join by using a separate table to link the genres to the books. Our publishers are linked to book by a one-to-many. This means that each book has one and only one publisher. For genres, each book can have many genres and each genre can be assigned to many books. This is many to many. The best way to handle that relationship is to have a table which contains the index from each of the tables and acts to link them together.

## Steps

### Database

1. Create a table called genres with fields genreId (nvarchar(40)) and genreName (nvarchar(20))
2. Create a tables called genresToBooks with genreId ((nvarchar(40)) and isbn13((nvarchar(15))
3. In the genres table, use uuids for the genreIds and put each of the genres your books use (or more) into the table. You can put these directly into the db at this point.

### Add/Edit Page: Form

1. At the top of the mainForm function, inside the \<cfif book neq ‘’>, We are going to add two function calls to `bookstore.cfc`. The first selects all the genres in genres and orders them by genreName and is called `allGenres`. The second selects all of the rows out of `genreToBook` where the `isbn13` is that same as the book which was submitted. Call this one `bookGenres`. The query involves a join between genreToBook, genres and books.
2. Add another `<div class="form-floating mb-3"></div>`

in the addEdit mainForm and Make the label `Genres` although you might need to make it outside the \<div>\</div> tags. We’re going to have two loops. The first loop is over the `allGenres` query. Here is the HTML you are looping over:

`<input id="genre#genreid#" type="checkbox" name="genre" value="#genreid#" /> #genrename#<br/>`

This will create a checkbox for each genre in our database. This will allow us to simply check the genres which apply to the book we are editing. Notice how it creates an id for each input which is “genre#genreid#” this means that the id for one of the inputs might look like this: “genreAA6D6981-F8E6-F683-74703DDB9CD5F031”. It also means that each input has a unique id. This is important for our second loop.\
3\. The second loop is for the query `bookGenres` and loops over this code:

`<script>document.getElementById('genre#genreid#').checked=true;</script>`

Remember that this query only has the genres which the book we are editing has assigned to it. Therefore, it will only check off the boxes for which this book has been assigned so that it will be visible to the user. Make sense? Look at the demo at [https://comweb.uml.edu/CodeBase/week9/](https://comweb.uml.edu/CodeBase/week9/) to see it (you’ll have to make an account to get to the management page)

### Add/Edit Page: Submission

1.  We are already handling the submission of our addEdit.cfm mainForm in the processForms function in addEdit.cfc, right? So to accommodate adding and removing genres, we need to expand that function. There are two steps to handling the genre submission

    1. We need to somehow remove all the genres which are no longer assigned to this book and
    2. We need to add the genres which have been assigned to the book.

    To do this, we’re going to add two functions to our addEdit.cfc and call them from processForms. There is no set place to put this so perhaps right after the uploadImage section put this:

    ```
    if(formData.keyExists("genre")){
       deleteAllBookGenres(formData.isbn13);

       formData.genre.listToArray().each(function(item){
          insertGenre(item, formData.isbn13);
       });
    }
    ```

    Can you figure out what this does? Now create the `deleteAllBookGenres` function. It’s sole purpose is to contain a query which deletes all of the genres from `genresToBooks` for the book we are editing. Since this is the first time we are using a DELETE in a query, let me refresh your memory and give you the SQL:

    `delete from genrestobooks where isbn13='#form.isbn13#'`

    This removes all of the genres assigned to this book so that we can add any of the items which have been assigned to it. Don’t forget to paramaterize the query.
2. If multiple genres are submitted they well be in a list, separated by a comma like this: `14823C92-2D7D-499D-8658A584655A8657,82A521AD-852C-4457-AB339A3E77CF19C9.`

See how there is a comma half way through? After deleting the existing genres, we are going to loop over this list and insert one record for each item in the list. In the tag format, we used \<cfloop> \</cfloop>. However, since we’re in script, we have to use a different format. In this case, we’re going to use something called “Higher Order Functions”. Without going too much into the meaning behind that, this is the next line in the code:

```
formData.genre.listToArray().each(function(item){
   insertGenre(item, formData.isbn13);
});
```

which is definitely going to involve some unpacking.

`formData.genre`: This is the list of genres which were passed from the form

`.listToArray():` This converts the list of genre ids to an array.

`.each( )`: This is a built in function that will take each item in the array (created by listToArray()) and run it through the function inside the ( );

`function( item ){ insertGenre(item, formData.isbn13 }`: This will run the function “insertGenre” and pass in the current genreId as “item” as well as the formData.isbn13. We need to create the insertGenre function. It will accept the genreid and the isbn13. Check out the CodeBase on the class website to get a example if you need a hand.

### GenreNav.cfm

The genrenav.cfm currently has a hardcoded list of genres in it. We want a list of each genre for which there is a book in the database. For example, if there is a genre for “Underwater Basket Weaving” but we have no books on that topic, we do not want to list the genre in our genre nav. What would be the point? Conversely, if we have 50 books on any topic, we don’t want that genre to show up 50 times. We want each genre with a book to be displayed once. To do that we are going to use the “DISTINCT” key word.

1. At the top of the genreNav.cfm page, call a function in the bookstore.cfc which has this query: `select distinct genres.genreid, genrename from genrestobooks inner join genres on genres.genreid = genrestobooks.genreid order by genrename`
2. In the current genreNav.cfm, replace the hardcoded \<li> tags with a loop over something like this: `<li class="nav-item"><a class="nav-link" href="#cgi.SCRIPT_NAME#?p=details&genre=#genreid#">#genrename#</a></li>`

Notice how they open our existing details.cfm module but pass in a new variable called “genre”. Don’t forget to wrap the loop in a \<cfoutput>\</cfoutput>

### Details.cfm

The details page needs to be only marginally tweaked. The first thing to do is to add another \<cfparam> tag at the top of the page for the genre variable and have it default to “”.

`<cfparam name="genre" default="" />`

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
