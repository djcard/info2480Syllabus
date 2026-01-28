# Assigning Genres to a Book in our AddEdit.bxm page

### Getting the Data We Need

1. In our addEdit.bxm page near where we set allPublishers and bookInfo,  we are going to set two more variables. The first will hold all of the genres in the genres table . The second selects all of the rows out of `genreToBook` where the `isbn13` is that same as the book which was submitted. Call this one `bookGenres`.  \
   \<bx:set allGenres = common.allGenres() />\
   \<bx:set bookGenres = common.

## Creating the Genres Inputs

1. Add another `<div class="form-floating mb-3"></div>` . Put a \<div> over it that has the label Genres.
2. Inside that \<div> we are going to loop over the data we have in allgenres and use it to create a checkbox for each of the genres in our database.\
   `<bx:loop query="allGenres">`\
   &#x20;    `<input id="genre#id#" type="checkbox" name="genre" value="#id#" /> #name#<br/>`\
   `</bx:loop>` \
   \
   There are a few things to note here\
   1\. All of these checkboxes will have the same name. This is intentional and the reason will become clear very soon. \
   2\. Each of the checkboxes have a unique id in a predictable way. This is also intentional and the reasons for this will become clear as well. &#x20;

&#x20;When you open the page in your browser you should see something like this: <br>

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

\
3\. The second loop is for the query `bookGenres` and loops over this code:

`<script>document.getElementById('genre#genreid#').checked=true;</script>`

Remember that this query only has the genres which the book we are editing has assigned to it. Therefore, it will only check off the boxes for which this book has been assigned so that it will be visible to the user. Make sense? Look at the demo at [https://comweb.uml.edu/CodeBase/week9/](https://comweb.uml.edu/CodeBase/week9/) to see it (you’ll have to make an account to get to the management page)

### Add/Edit Page: Submission

We are already handling the submission of form data at the top of the page inside the section checking if we've submitted the input isbn13. <br>

```boxlang
<bx:if form.keyExists("isbn13")>
...
</bx:if>
```

After we handle the image upload we will handle the genre submission.&#x20;

1. Add an if statement checking if we've submitted the `genre` input.&#x20;
2. Use the function clearAllBookGenres in our bookstore.common.books class to delete all of the records in our genresToBooks table for the submitted ISBN13.&#x20;
3. We are then going to loop over the genres which have been submitted and insert them one by one in the DB using the saveGenreToBook function we created.&#x20;



When multiple inputs have the same name in a form, their values are sent together as a comma separated list to the server. In our genres form above, if multiple checkboxes are checked, say for those with the values 4,8, and 10. The data is sent to the server with the format -  genre:4,8,10. We can then take that value and process it like we need to. To do that we are going to first convert that list into an array and then we are going to use a built in function (BIF) called `each`.  Each is one of several BIFs which doesn't accept a value such as a number, string or structure as an argument but, instead, accepts a function as an argument. As it loops over the values in our array, it will feed this function the values in the array, one by one and this passed in function will process the items in the array. Functions which accept functions as arguments are called "Higher Order Functions". The function which is passed is called a "callback function".

The code to call. Just to mix it up a little bit, let's write it in script on our template page, using the \<bx:script> ... \</bx:script>

```
<bx:script>
if(form.keyExists("genre")){
   common.clearAllBookGenres(form.isbn13);

   form.genre.listToArray().each(function(item){
      common.saveGenreToBook(item, form.isbn13);
   });
}
</bx:script>
```

The saveGenreToBook function will run one time for each genre that is submitted.&#x20;
