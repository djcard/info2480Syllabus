# Creating The Manage Books Page

Our Manage Book tool is called addEdit.bxm and has the same basic layout as the manageArticles.bxm page. On the left will be a list of the books in the database and on the right will be the form that allows us to enter or edit the data in our db. As you work through these steps, use the existing articles.bx and manageArticles.bxm as a model.&#x20;



### In addEdit.bxm

1. Using manageArticles.bxm as a model, use the row and col classes in Bootstrap to create a left column ( col-3 ) and a column ( col-9 ).
2. Again, using manageArticles.bxm as a model, create a form which has one control ( \<input /> )  for each field in your books table except for the publisherId. This might include the title, ISBN13, ISBN, year, weight, and pages.&#x20;

### Create our Data Functions

1. Create a new class file in the bookstore/common folder called `books.bx`.
2. Create 2 functions in `books.bx`. Call the first `saveBooks` and the second `searchBooks`.
3. Using articles.bx as a model, write the SQL to save a new book to the db in the `saveBooks` function.&#x20;
4. Again, using articles.bx as a model, write the searchBooks function so that you can either return all books in the books table or search on the title or isbn13 field.&#x20;



`Back in addEdit.bxm`

1. Create the side navigation which lists all the books in your database. Make each item be a link to use the addEdit.bxm template and send the isbn13 of the book through the address bar.
2. Use the submitted isbn13 to retrieve the book details from the database and populate the form so you can edit the book.&#x20;
