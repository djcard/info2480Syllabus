# End of Project Checkllist

Over the past several sessions, we've created several dynamic tools that allow our booksttore's staff to manage the books they sell and for customers to find the books they want. This is a checklist that your site should have broken down by pages. Even if your pages don't match this exactly, all of this functionality should be present to have a complete project.&#x20;

## The Front Facing Application

### Front Page - bookstore/public/index.bxm

* [ ] The html, head and body tage for the front facing application
* [ ] Links / references to the Bootstrap library and any other CSS you wish to use
* [ ] Should include the header
* [ ] Should include the horizontalnav
* [ ] Should include the genreNav
* [ ] Should include the footer
* [ ] Should include a dynamic section where the content changes based on the module sent ( the t variable if you followed the docs )
* [ ] By default the dynamic section should display either the carousel or another module of your choice

### Header - bookstore/public/header.bxm

* [ ] The name of your store or any extra styling you wish
* [ ] Links to one or more articles which opens content.bxm in the dynamic area
* [ ] A search form which opens details.bxm in the dynamic area

### Footer - bookstore/public/footer.bxm

* [ ] Any thing you want to put in the footer

### Carousel - bookstore/public/carousel.bxm

* [ ] Display a rotating selection of books or other content

### Genre Nav - bookstore/public/genreNav.bxm

* [ ] Should display a list of genres
* [ ] Genres should only be included if there is a book in the books table assigned to that genre.

### Details - bookstore/public/details.bxm

* [ ] Should display the results of the search started by the form in the horizontalNav
* [ ] Should search on the title, ISBN13 or the genreid submitted
* [ ] Should show a list if there are multiple results where the title is a link to view the details of the book.
* [ ] Should show a message if there are no books found
* [ ] Should show the details of the book if there is one result in the search. This should include
  * [ ] Title of the book
  * [ ] An image
  * [ ] A description of the book
  * [ ] The publisher ( which can also be a link to show all books from that publisher )
  * [ ] Any genres to which the book has been assigned
  * [ ] The year of publication and any other info about the book you wish to display

## The Management Tools

### Front Page - bookstore/manage/index.bxm

* [ ] The html, head and body tage for the management application
* [ ] Links / references to the Bootstrap library and any other CSS you wish to use
* [ ] Should include the horizontalnav
* [ ] Should include a dynamic section where the content changes based on the module sent ( the t variable if you followed the docs )
* [ ] By default the dynamic section should display either the manageArticles.bxm or the addEdit.bxm page

### Horizontal Nav - bookstore/manage/horizontalNav.bxm

* [ ] A link to the manageArticles.bxm module
* [ ] A link to the addEdit.bxm module

### Manage Articles - bookstore/manage/manageArticles.bxm

* [ ] Display a list to create a new article
* [ ] Display a list of articles in the database
* [ ] When the new article link is clicked or an article chosen, display the edit form
* [ ] The edit form should include the id of the article, the title and the description
* [ ] The description should be a WYSIWYG tool.

### Add / Edit Books - bookstore/manage/addEdit.bxm

* [ ] Display a new book link
* [ ] Display all books in the database
* [ ] When a new or current book is chosen, display the edit form
* [ ] The edit form should include:
  * [ ] ISBN-13
  * [ ] Title
  * [ ] Publisher - This is a select control with the options dynamically populated from the publishers table
  * [ ] Description - This is a text area which has WYSIWYG tools attached
  * [ ] Displays the cover of the book
  * [ ] Has an input to upload a new book cover
  * [ ] Displays a dynamic list of genres in the database
  * [ ] Has the genres to which the book has been applied checked off.





