# Assigning Genres in our AddEdit.bxm page

### Add/Edit Page: Form

1. In our addEdit.bxm page near where we set allPublishers and bookInfo,  we are going to set two more variables. The first will hold all of the genres in the genres table . The second selects all of the rows out of `genreToBook` where the `isbn13` is that same as the book which was submitted. Call this one `bookGenres`.  \
   \<bx:set allGenres = common.allGenres() />\
   \<bx:set bookGenres = common.
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
