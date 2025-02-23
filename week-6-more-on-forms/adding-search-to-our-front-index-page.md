---
hidden: true
---

# Adding Search To Our Front Index Page

## Background

On the front page of our website is a form which we put into the navigation bar during the first few weeks of class. We are now going to make that form do something. When the user submits the form, the site will open myfinalproject/index.cfm with a results module which will either show the details of the book they chose, tell them that there was were no results if there weren’t any or give them a list of the books that fit the criteria if there are more than one.

## Assignment

There are two parts to creating the search functionality to your site. This assignment assumes that you’ve already separated your index page into its component pieces using \<cfinclude>. If you haven’t, please do that first. These directions will make more sense if you do. It’s also expected that you adapted the management page to include the image and publisher fields.

There are two parts to this assignment:

1. Adapting the form on the front page of the site
2. Adapting our index page to use “modules”
3. Creating a detail page to display the results.

### Adapting the Front Form

1. Open the file which has the top navigation system for your site. This might be in header.cfm or whatever you named it when you split up your page into parts.
2. Find the form in the navbar that is meant to be the search form. Currently the \<form> looks like this:\
   `<form class="d-flex" action="#cgi.script_name#?p=details" method="post"> <input class="form-control me-2" type="search" name="searchme" placeholder="Search" aria-label="Search"> <button class="btn btn-outline-success" type="submit">Search</button> </form>`

The form was there as a place holder and was based on the navbar example at[http://getbootstrap.com](http://getbootstrap.com).\
3\. In the \<form> add the action="#cgi.SCRIPT\_NAME#?p=details" method=”post” to the tag. We’ve already gone over what these mean so we don’t need to do it again. You might also need to wrap the form in \<cfoutput> tags. Do you know why? 4. Add name="searchme" to the \<input> tag inside the form.

Done with the front form!

### Adapting our index page

On the public facing index page, there is the line which includes the carousel page.

\<cfinclude template = ”carousel.cfm” />.

That needs to be adapted to show different pages based on what is submitted. We do this like this:

\<cfinclude template = ”#p#.cfm” /> The variable p in this case stands for “page”. This means the variable P should correspond to the name of a page in that folder. However, what do we do if the user has never been to the page before? We need to make sure that “p” always exists.

We do that by adding the line \<cfparam name=”p” default=”carousel” /> to the top of the page. This ensures that if “p” is submitted via a form or the URL that that value will be used but if no “p” is established, the page will create one and give it the default value of “carousel” which will open the carousel.cfm page.

Done with that section!

### Creating the Results Page

The majority of the results page will be up to your discretion in terms of layout. However, there are a couple of elements to walk through here first.

1. Create a new page in your MyFinalProject folder called details.cfm.
2. Remove all the HTML tags from the page and add a \<cfdump var=”#form#”> to the page. Save and upload it to your site.
3. Open your index page and type a keyword into the search box. Submit it. Does the detail page appear with the form variables dumped out? There should be one variable called “Searchme”. Did it work? If not, figure out why and get that working before proceeding.
4.  Create a bookstore.cfc file in your MyFinalProject folder. This will be the controller for the front end of the site. Create a connection to the controller on the index.cfm page by adding

    `<cfset bookstoreFunctions = createObject("bookstore") />`
5. \*\*\*\*in bookstore.cfc create function called obtainSearchResults and in it create the following query:\
   `select * from books inner join publishers on books.publisher=publishers.id where title like '%#trim(form.searchme)#%' or isbn13 like '%#trim(searchme)#%'`
6. Call obtainSearchResults from details.cfm. Use a variable called “bookInfo”. It look like this:

`<cfset bookInfo = bookstoreFunctions.obtainSearchResults( form.searchme ) />`

7. Most of this should be very clear by now but the second line is new. Why are we searching on both the title and the ISBN? What does inner join mean???? SQL Server is a relational database. This means that SQL statements can be written that join data from one table with data in another table. In this case, we are telling SQL server to give us all of the fields in books AND in publishers where the value in the publishers field in books is exactly the same as the id field in publishers. This makes sense since we used the id field in publishers to populate the publisher field in books for just this purpose. It’s important to remember that INNER JOIN means that SQL server will only give results if it finds a value in common in BOTH tables. **If there is a book with no publisher value, no results will be returned.** Let me reiterate that:  **If there is a book with no publisher value, no results will be returned.**
8.  When searching for a book, there are three possible results.

    1. There are no results
    2. There is one result
    3. There is more than one result Therefore, in your details page, set up the following:

    `<cfif bookinfo.recordcount == 0> #noResults()# <cfelseif bookinfo.recordcount == 1> #oneResult()# <cfelse> #manyResults()# </cfif>`
9. At the bottom of the page, create a function named “noResults” and put “There were no results to be found. “ inside of it. Do the same with “oneResult” with “There was one result, show the details” and “manyResults()” and “There were more than one result, show a list.”
10. Save and upload both the header.cfm page and your details page. Open the index.cfm page in a browser and enter a value into the search box on the main page. Did you get the results you thought you would?
11. NO Results: This is the more straightforward part of this process. Enter a polite message for the user to try again. You can add other things if you wish but it isn’t necessary for our purposes here.
12. More than one result: This means that multiple books fit the user’s request. We need to give them a list of the results and let them choose the one they choose. This is done with a few lines of code:\
    `<ol class="nav flex-column">` `<cfoutput query=”bookinfo”> <li` `class="nav-item"> <a class="nav-link" href=”#cgi.script_name#?p=details&searchme=#trim(isbn13)#”> #trim(title)# </a> </li> </cfoutput> </ol>`

Does that answer the question about searching on both the ISBN13 and the title? HOWEVER, when we are submitting from the form on the front page, we are passing in FORM.searchme and when we are searching from the hit list we are passing in URL.searchme. Problem? Potentially, but we can solve it by adding \<cfparam name=”searchme” default=””> and changing our query to use isbn13=’#searchme#’ instead of isbn13=’#form.searchme#’. The \<cfparam> tag will look for a variable called “searchme” in a number of different scopes (such as URL and FORM) and set the general variable called “searchme” to whichever it finds. 13. One result: This is what we are going for. If there is one result we can do a layout that shows the details of the book we want to highlight. Here is a start:\
`<cfoutput> <img src="images/#bookinfo.IMAGE[1]#" style="float:left; width:250px; height:250px" /> <span>Title: #bookinfo.title[1]#</span> <span>Publisher: #bookinfo.name[1]#</span> </cfoutput>`

Notice how we have data from two different tables showing up from one query. Nice job. See it’s fun! Way to **join** the party! (See what I did there???)

Well done. Is this coming together?
