# Adding Search To Our Front Index Page

## Background

On the front page of our website is a form which we put into the navigation bar during the first few weeks of class. We are now going to make that form do something. When the user submits the form, the site will open `bookstore/public/index.bxm` with a results module which will either show the details of the book they chose, tell them that there was were no results if there weren’t any or give them a list of the books that fit the criteria if there are more than one.

## Assignment

There are two parts to creating the search functionality to your site. This assignment assumes that you’ve already separated your index page into its component pieces using \<bx:include>. If you haven’t, please do that first. These directions will make more sense if you do.&#x20;

There are two parts to this assignment:

1. Adapting the form on the front page of the site
2. Creating a detail page to display the results.

### Adapting the Front Form

1. Open the file which has the top navigation system for your site. This might be in header.bxm, horizontalNav.bxm or whatever you named it when you split up your page into parts.
2. Find the form in the navbar that is meant to be the search form. Currently the \<form> looks like this:\
   `<form class="d-flex">` \
   &#x20;    `<input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">` \
   &#x20;     `<button class="btn btn-outline-success" type="submit">Search</button> </form>`

The form was there as a place holder and was based on the navbar example at [http://getbootstrap.com](http://getbootstrap.com).\
3\. In the \<form> add the action="#cgi.SCRIPT\_NAME#?t=details" method=”post” to the tag. We’ve already gone over what these mean so we don’t need to do it again. You might also need to wrap the form in \<bx:output> tags. Do you know why?&#x20;

4\. Add name="searchTerm" to the \<input> tag inside the form.

Done with the front form!

### Creating the Results Page

The majority of the results page will be up to your discretion in terms of layout. However, there are a couple of elements to walk through here first.

1. Create a new page in your `bookstore/public/` folder called `details.bxm`.
2. On the blank details.bxm page, add a \<bx:dump var=”#form#”> to the page and save it.
3. Open your index page and type a keyword into the search box. Submit it. Does the detail page appear with the form variables dumped out? There should be one variable called “searchTerm”. Did it work? If not, figure out why and get that working before proceeding.
4.  Create a connection to the bookstore.common.books class on the index.bxm page by adding

    `<bx:set bookstoreFunctions = createObject("bookstore.common.books") />`
5. In book.bx, we have already made a function called searchBooks which should look something like this: \
   `select * from books where title like '%#trim(form.`searchTerm`)#%' or isbn13 like '%#trim(searchme)#%'`\
   Most of this should be very clear by now but the second line is new. Why are we searching on both the title and the ISBN? <br>
6. From details.bxm, call bookstoreFunction.searchBooks() and pass in form.searchTerm. Use a variable called “bookInfo”. It should look similar to this:

`<bx:set bookInfo = bookstoreFunctions.searchBooks( form.`searchTerm`) />`

7.  When searching for a book, there are three possibilities.

    1. There are no results
    2. There is one result
    3. There is more than one result Therefore, in your details page, set up the following:

    ```boxlang
    <bx:output>
        <bx:if bookinfo.recordcount == 0> 
            <bx:include template="noResults.bxm" />
        <bx:elseif bookinfo.recordcount == 1> 
            <bx:include template="oneResult.bxm" />
        <bx:else> 
            <bx:include template="manyResults.bxm" />
        </bx:if>
    </bx:output>
    ```
8. Create the three files (noResults.bxm, oneResult.bxm, and manyResults.bxm)&#x20;
   1. In noResults.bxm put “There were no results to be found. “.&#x20;
   2. In oneResult.bxm put “There was one result, show the details”&#x20;
   3. In manyResults.bxm put “There was more than one result, show a list."\
      \
      It's not strictly necessary to make a new file for each scenario. We could put our HTML for each scenario directly into details.bxm but in order to keep our file small and also to follow patterns created by some JS Libraries like React, Vue or Next.js, we are going to keep our HTML in as small templates as possible.
9. Save your files, make sure your site is running and open the index.bxm page in a browser. Enter a value into the search box on the main page. Did you get the results you thought you would?

### noResults.bxm

NO Results: This is the most straightforward part of this process. Enter a polite message for the user to try again. You can add other things if you wish but it isn’t necessary for our purposes here.

### manyResults.bxm

More than one result: This means that multiple books fit the user’s request. We need to give them a list of the results and let them choose the one they choose. This is done with a few lines of code:\
`<ol class="nav flex-column">` \
&#x20;    `<bx:output query="bookinfo">` \
&#x20;   `<li` `class="nav-item">` \
&#x20;       `<a class="nav-link" href="#cgi.script_name#?p=details&searchTerm=#trim(isbn13)#">` \
&#x20;           `#trim(title)#` \
&#x20;       `</a>` \
&#x20;   `</li>` \
&#x20;   `</bx:output>` \
`</ol>`

Does that answer the question about searching on both the ISBN13 and the title? HOWEVER, when we are submitting from the form on the front page, we are passing in FORM.searchTerm and when we are searching from the hit list we are passing in URL.searchTerm. Problem? Potentially, but we can solve it by adding \<bx:param name=”searchTerm” default=””> and changing our query to use isbn13=’#searchTerm#’ instead of isbn13=’#form.searchTerm#’.&#x20;

The \<bx:param> tag will look for a variable called “searchTerm” in a number of different scopes (such as URL and FORM) and set the general variable called “searchTerm” to whichever it finds.&#x20;

### oneResult.bxm

This is what we are going for. If there is one result we can do a layout that shows the details of the book we want to highlight. Here is a start:\
`<bx:output>` \
&#x20;   `<div>Title: #bookinfo.title[1]#</div>` \
&#x20;   `<div>Publisher: #bookinfo.ISBN13[1]#</div>` \
&#x20;   `<div>Year: #bookinfo.year[1]#</div>` \
&#x20;   `<div>Weight: #bookinfo.weight[1]#</div>` \
`</bx:output>`



Well done. Is this coming together?
