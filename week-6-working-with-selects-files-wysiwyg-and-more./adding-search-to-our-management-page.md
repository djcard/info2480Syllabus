---
hidden: true
---

# Adding Search To Our Management Page

## Background

We can now add and edit books in our books table. That means we can hire a staff to start entering books as fast as possible. It didn’t take too long, about 20 min, before the list of books on the left of our add/edit page had so many items that it was taking a long time to scroll and find the books they wanted to edit. They counted and there were only 100 in the system and they had about 1000 more to go. How to solve this?

Obviously, we cannot list the entire contents of the books table every single time we use the page if it is going to be that long. Therefore, let us add a search function onto the management page so we can search for the book we want to edit.

## Overall Process

We’re going to add a search form to the SIDENAV method on our addedit.cfm module. This search form will filter the books in our database and present a subset of books from which we can choose to edit.

This means that we are going to be passing in several parameters into the page at one time. We will still have the “tool” parameter which dictates what module is going to open. We have the parameter “book” which is the book which we have chosen to edit. Now we are going to add another parameter called “qterm” which we are going to use as the phrase used to present book titles from which to choose to edit.

## Adding a Search Form

1. Open your addedit.cfm page in the management folder
2. At the top of the page add a \<cfparam name=”qterm” default=’’>
3. At the bottom of the page, outside of all the functions, add new function called “findBookForm” which contains a small form with one input called qterm.
4. Here is a sample with the Bootstrap classes in place:

```
<cffunction name="findBookForm">
    <cfoutput>
        <form action="#cgi.script_name#?tool=#tool#" method="post">
            <div class="form-floating mb-3">
                <input type="text" id="qterm" name="qterm" class="form-control" value="#qterm#" placeholder="Enter a search term to find a book to edit" />
                <label for="qterm">Search Inventory </label>
            </div>
        </form>
    </cfoutput>
</cffunction>
```

1. Make a call to this form from inside your sideNav function: \<cffunction name=”sideNav”> \<cfset findBookForm()> \<cfset allbooks=addEditFunctions.sideNavBooks()>

## Handling the Search Submission

By default, the list on the side will be blank until we search. When we search for a book to manage, we are going to be submitting an input with the name qterm. We only want to search for books to manage if qterm has been submitted.

1.  Adapt the call addEditFunctions.sideNavBooks() in addEdit.cfm to pass in the qterm value

    `<cfset allBooks = addEditFunctions.sideNavBooks( qterm ) />`
2. In addEdit.cfc, add an if / else to our sideNavBooks() function. We’re only going to run the query if there actually is a qterm passed in. We can use the length of the qterm string passed in as our test. `if(qterm.len() ==0){ do this if there is no qterm } else { here is where our current query goes }` In addEdit.cfc, in the sideNavBooks function, change the sql to:

`select * from books **where title like :qterm** order by title`

and add the needed parameter:

`addParam(name="qterm",value="%#qterm#%");`

See how we adapted the parameter to mimic the “like” syntax with the wildcards ( % ) ? 3. Do a search and see if the list starts off blank and then presents a list of books when you enter a search term. See an error? We missed a step. 4. Since we put the `if` around the query, if qterm is an empty string, the query doesn’t run. If it doesn’t run, then the query results don’t exist. If the query results don’t exist, then, when we loop over the query “allbooks”, we will get an error since the query allbooks doesn’t exist. What we need to do is have allbooks return a query with no results so our code has something to loop over. This code

`return queryNew("title");`

will return an empty query with one column: “title”.

We now have 3 possible scenarios in our sideNav. 1. There is no search term entered 2. There were no results 3. There were results and we should list them.

```
We can accommodate all three scenarios like this:

`<cfif qterm.len() ==0>

<cfelseif allbooks.recordcount==0>

<cfelse>

</cfif>`
```

The sideNav Function now looks something like this:

```
<cffunction name="sideNav">
    <cfset allBooks = addEditFunctions.sideNavBooks( qterm ) />
    <div>
        Book List
    </div>
    <cfoutput>
        #findBookForm()#
    </cfoutput>
    <cfoutput>
        <ul class="nav flex-column">
            <li class="nav-item">
                <a href="#cgi.script_name#?tool=addedit&book=new" class="nav-link">
                    New Book
                </a>
            </li>
            <cfif qterm.len() ==0>
                No Search Term Entered
            <cfelseif allBooks.recordcount==0>
                No Results Found
            <cfelse>
                <cfloop query="allBooks">
                    <li class="nav-item">
                        <a href="#cgi.script_name#?tool=addedit&book=#isbn13#" class="nav-link">#trim(title)#</a>
                    </li>
                </cfloop>
            </cfif>
        </ul>
    </cfoutput>
</cffunction>
```

SideNavBooks() looks something like this:

```
function sideNavBooks( qterm ){
   if(qterm.len() ==0 ){
      return queryNew("title");
   } else {
      var qs = new query(datasource = application.dsource);
      qs.setSql("select * from books where title like :qterm order by title");
      qs.addParam(name="qterm",value='%#qterm#%');
      return qs.execute().getResult();
   }
}
```

## Remembering the Search

If we enter a search term, we might want the page to remember it so we don’t have to keep typing the search over and over again. We might not but let’s put that feature in as an exercise.

1. In the qterm \<input> tag add value=”#qterm#”. If qterm is blank, this will simply stay blank. Remember that qterm always exists so we don’t run into a problem of this breaking from qterm not being set.
2. Change the \<a> for the booklist items on the left side to: href=”cgi.SCRIPT\_NAME#?tool=addedit\&book=#isbn13#**\&qterm=#qterm#”**
3. Change the action of the mainForm to #cgi.script\_name#?tool=addedit\&qterm=#qterm# and achieved the same result.
4. Upload all of that. Did it work? Why did we have to make ALL of those changes to keep our search phrase intact?
5. Check out the CodeBase on the class site to see the latest iteration of the code.
