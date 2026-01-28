---
hidden: true
---

# Expanding And Styling The Main Form

## Background

Last week, we created a form that allowed us to enter an ISBN and a title and then put that title and ISBN into the database. This week we’re building on that and putting in some style.

## Adding Bootstrap Styles

We are going to style our form after the “Horizontal Form” which is in Bootstrap. To do this is not terribly complicated, the hardest part is just getting the HTML correct.

1. For each Inputs in your Main Form form

Each input should follow more or less the same HTML style. In this case, we’re using the Floating Labels structure as seen at [https://getbootstrap.com/docs/5.1/forms/floating-labels/](https://getbootstrap.com/docs/5.1/forms/floating-labels/). You are welcome to use whatever structure you like but be consistent. I’ve put the new parts in bold. For this layout. It’s essential the the input comes BEFORE the label.\
\`

```html
**<div class="form-floating mb-3">**
    <input type="text" id="isbn13" name="isbn13" **class="form-control"** value="" placeholder="Please Enter The ISBN13 of the book" />
    <label for="isbn13">ISBN 13: </label>
**</div>**

```

For the submit button, which has no label, one option i to make it stretch 100% across the page.

`<button type="submit" class="btn btn-primary" style="width: 100%">Add Book</button>`

How does that look? Does your form still submit correctly? If not, what changed? If it isn’t submitting correctly, check that the name properties are still present.

## Adding More Text Inputs

There are two parts to adding more text inputs:

1. Adding the input to the form
2. Making sure that the insert or update query handles the new data being submitted.

### Adding new Text Inputs

There are a few text inputs which we can add to our mainForm form just like we did in the last exercise which are the Year, Weight, ISBN, pages. Add these to your form with the bootstrap formatting. Don’t forget to pay attention to the name and id properties for each input.

For example, the HTML for the weight input would be:

```html
**<div class="form-floating mb-3">**
    <input type="number" id="weight" name="weight" step=".1" **class="form-control"** value="" placeholder="Please Enter The weightof the book" />
    <label for="weight">Weight: </label>
**</div>**
```

### Input Types

Note the new type=”number”. What are the different types of input and why are they important? Check out [https://www.w3schools.com/html/html\_form\_input\_types.asp](https://www.w3schools.com/html/html_form_input_types.asp) for more information about input types. In this case, we’ve changed the type for the weight input to “number”. Why?

### Adapting the query

Now we need to change our focus to our controller and handle all the new data coming from our form. In the processForms method, we have a query that inserts the title and the ISBN13 fields. Why did we choose those two fields? Well, the ISBN13 is our primary key so that needs to be there whenever a new book is inserted. The title is a good descriptor of the book that is “human readable” and makes it easy for us to tell one record apart from each other if we need to. Given these two criteria, it makes sense that we’d pick those two items to be inserted.

Do we want to add more to the insert record? Maybe or maybe not. We want to allow the maximum flexibility with the least amount of duplicate code. Since we’re giving users the ability to edit nearly all, if not all, of the fields in the database, we know that all of these are going to be in our UPDATE statement as well. Rather than duplicate many of the fields, let’s put the bare minimum into the INSERT statement and then put the majority of the fields in the update clause. What do I mean by this?

When we add a new record into the DB, we use the keyword INSERT in our sql. When we are updating, we use the keyword UPDATE. Therefore, we are going to need two SQL statements in our processForms function. With me so far?

We already created our INSERT function last week when we were inserting books into the DB. Currently it looks like this:

IF NOT **EXISTS**( SELECT \*\*\*\*\* **FROM** books **WHERE** isbn13=**:isbn13**) **INSERT INTO** books (isbn13,title) VALUES \*\*\*\*(**:isbn**,**:title**);

If we break that down again, it says, if we check the database for a book with the ISBN13 of formData.isbn13, then insert into the db this ISBN13 with this table. The ‘;’ signifies the end of the SQL statement. To keep the maximum flexibility with the least amount of code duplication, let’s put the majority of the fields in the UPDATE statement and only the fields we need to easily identify the record in the insert statement.

If we add the fields we just added, this would make our SQL look like this:

IF NOT **EXISTS**( SELECT \*\*\*\*\* **FROM** books **WHERE** isbn13=**:isbn13**) **INSERT INTO** books (isbn13,title) VALUES \*\*\*\*(**:isbn**,**:title**); UPDATE books SET\
title=:title, weight=:weight, year=:year,\
isbn=:isbn,\
pages=:pages\
WHERE isbn13=:isbn13

Let’s note a few things.

* The “set” items don’t need to be on separate lines, it just makes it easier to read
* The WHERE clause in the update statement is essential. Otherwise, each row in the DB will be updated with this new information.
* Once the INSERT function puts the ISBN13 in the DB, we can then use that to reference the correct row to put in the rest of the data.

However, this is only ½ the job. What does the “:isbn13” and “:pages” mean? We didn’t go into a whole lot of detail about that last week.

When we looked at SQL originally we said that an insert statement looked like this:

Insert into table ( field1, field2, field3 ) values ( ‘:value1’, ’:value2’, ’:value3’ );

When we are using a variable it looks like this:

Insert into table ( field1, field2, field3 ) values ( ‘#value1#’, ’#value2#’, ’#value3#’ );

This works well. However, there is a better way to do this that takes advantage of something called SQL Bind Parameters. This is another way of passing data to the database that has a couple advantages over simply putting the data into the sql query directly.

1. It is more secure since it provides some validation before the data is inserted into the database. This allows us to check the datatype of the data we’re sending before we send it. If it is expecting a number and our query is trying to send some text, we can stop the query before it runs.
2. It also makes for faster queries. For the size queries we are doing it might not make that much of a difference but for more complex queries or websites that have more traffic the speed differences would add up.

As a result we need to add a qs.addParam()for all of the new items in our form as well.

Can you figure out how to do it? The whole function should now look like this:

```
function processForms( required struct formData ){

		if ( formData.keyExists( "isbn13" ) && formData.isbn13.len()==13 && formData.title.len() > 0) {
			var qs = new query(datasource=application.dsource);
			qs.setSQL("
			IF NOT EXISTS( SELECT * FROM books WHERE isbn13=:isbn13)
        		INSERT INTO books (isbn13,title) VALUES (:isbn13,:title);
			UPDATE books SET
    			title=:title,
    			weight=:weight,
    			year=:year,
    			pages=:pages
				WHERE isbn13=:isbn13
			");
			qs.addparam(name="isbn13",cfqsltype="CF_SQL_VARCHAR",value=formData.isbn13,**null=formData.isbn13.len()!=13** );
			qs.addparam(name="title",cfqsltype="CF_SQL_NVARCHAR",value=formData.title,**null=formData.title.len()==0** );
			qs.addParam(name="weight",CFSQLTYPE="CF_SQL_NUMERIC",value=formData.weight);
			qs.addParam(name="year",CFSQLTYPE="CF_SQL_NUMERIC",value=formData.year);
			qs.addParam(name="pages",CFSQLTYPE="CF_SQL_NUMERIC",value=formData.pages);
			qs.execute();
		}
	}
```

Try updating a few records. Does it work?

### General Concept: Defensive Coding

Defensive Coding is concept where you write your code anticipating what can go wrong. I’m not sure there is anything called “offensive coding” although there can certainly be some general musings about what that would entail. In the above code snippet there are a few phrases bolded such as

`&& **formData.isbn13.len()==13 && formData.keyExists("title") && formData.title.len() > 0**`

and

**`null=formData.isbn13.len()!=13`**

and

**`null=formData.title.len()==0`**

These are specific touches put into to protect the data in our data base. The first line adds an additional check as to whether it should or should not run our query. We were already checking whether the formData.isbn13 been submitted at all. Now we’re adding an additional check that says not only does formData need to have an 1sbn13 key, but the value of that key needs to be exactly 13 characters long. FormData also needs to have the key “title” and that title can not be blank. How does this protect the data in our DB?

There is the additional protection of the “null=: phrase as part of the parameter. This tells the query to insert a null into the database if certain conditions are met. This can be helpful in many scenarios as a last defense if the data has gotten this far. However, this does not send any message back to the user so they can fix their entry and is designed to “fail silently”. This isn’t very helpful if these checks are on two columns which are required such as ISBN13 or TITLE. In most respects, it’s better to deal with bad data earlier than this. In our function here, the “null=” code should never come into play but it’s there as an example.

What happens if some data is submitted that does not make it through our defensive coding? We have an `if` to check for data, if that’s the case, we should probably have an `else` to let the user know their information wasn’t saved. At the end of processForms function, let’s add this else statement.

```
    qs.addParam(name = 'image', CFSQLTYPE = 'CF_SQL_NVARCHAR', value = formData.image);
    qs.execute();
} **else {
    writeOutput("Information not saved! Check the ISBN or title ");
}**
```

## Updating Books Already in our DB

To edit and update books already in our DB, there are two steps.

1. We need to be able to select the book we want to edit and
2. We need to put the already existing values into our form so we only need to type in the values we want to change.

### Choosing a book from the left hand menu

Last week we created the sideNav that listed the books but currently it doesn’t do anything when you clicked on the title. The function looked like this:

```
<cffunction name="sideNav">
    <cfset allBooks = addEditFunctions.sideNavBooks() />
    <div>
        Book List
    </div>

    <cfoutput>
        <ul class="nav flex-column">
            <cfloop query="allBooks">
                <li class="nav-item">
                    <a class="nav-link">#trim(title)#</a>
                </li>
            </cfloop>
        </ul>
    </cfoutput>

</cffunction>
```

First we queried the database to get all the books in the DB. Then we looped over the query and created a \<li>\<a> \</a>\</li> for each row in the DB. We need to adapt this have an actual link.

The link needs to do three things.

1. Open up the correct page
2. Pass in the correct module to open
3. Pass in the correct book to find.

To do all of that, here is what the URL looks like

`<a class="nav-link" href=”#cgi.script_name#?tool=addedit&book=#isbn13#”>#title#</a>`

Let’s break that down.

| Code               | Description                                                                                                                                                                                                                                 |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| #cgi.script\_name# | This is a variable that contains the path and the name of the script (.cfm page) that is open. Since we want our page to simply reload itself, this works well and can be moved all over the site and will always open the same page again. |
| ?                  | This separates the address of the page from the query string                                                                                                                                                                                |
| tool=addedit       | This sends in a parameter called “tool” which is the name of the page we want to open in the module area.                                                                                                                                   |
| book=#isbn13#      | This is where we pass in the isbn13 of the book we want to edit.                                                                                                                                                                            |

Makes sense?

However, we also need to add one more item? What if we want to add a new book again? We should have a link to that as well. Inside the \<ul> tag but before the \<cfloop> tag, add a list item for a new book:

```
<li class="nav-item">
    <a href="#cgi.script_name#?tool=addedit&book=new" class="nav-link">
        New Book
    </a>
</li>
```

The latest version of our sideNav now looks like this:

```
<cffunction name="sideNav">
    <cfset allBooks = addEditFunctions.sideNavBooks() />
    <div>
        Book List
    </div>

    <cfoutput>
        <ul class="nav flex-column">
            <li class="nav-item">
                <a href="#cgi.script_name#?tool=addedit&book=new" class="nav-link">
                    New Book
                </a>
            </li>
            <cfloop query="allBooks">
                <li class="nav-item">
                    <a href="#cgi.script_name#?tool=addedit&book=#isbn13#" class="nav-link">#trim(title)#</a>
                </li>
            </cfloop>
        </ul>
    </cfoutput>
</cffunction>
```

Check out the URL. You should see that the ISBN of your books are being send in the address bar.

`/index.cfm?tool=addedit&book=9781933390000`

You might also be noticing that nothing is happening to our form when we do this. It will after the next section.

### Update Our Form With New Values

Once we are sending the ISBN13 of the book we want to edit, we can then use that information to query the database and populate our form.

If we are going to be querying the database each time the page opens, we will run in to an error if it is trying to use the ISBN of a book and that value hasn’t been submitted. Therefore, we need to make sure that there is a value to use at all times. To do that, we are going to add a \<cfparam> tag at the top of the page. The \<cfparam name=”book”> tag examines all the different scopes on the page (form, url, session, application etc) and looks for a variable which the same name as it is given. In the example here, the name=”book”. If there is no variable called “book” anywhere to be found, it will make one.  That way, the variable will be accessible for us to use.

At the top of your addedit.cfm page, put this line:

\<cfparam name=”book” default=””>

This will look for a variable called book and, if it doesn’t exist, make it with the value of “”>

Now what do we want to happen? Well, if there is a variable called “book” and book is not “”, we want to search the database for that book. Makes sense? Follow the next steps to make the mainEdit form

Let’s set up our mainEdit form to only show up if book is not blank. In the top section of the page, change

<**cfoutput**>**#mainForm()#**\</**cfoutput**>

to

```html
<**cfif** book **neq ""**>     
    <**cfoutput**>**#**mainForm()**#**</**cfoutput**> 
</**cfif**>
```

In the addedit.cfc (our controller component), let’s make a new function called bookDetails. It should receive All it does is perform the query to find the book in the database. Here is what it should more or less look like:

```
function bookDetails(isbn13){
   var qs = new query(datasource=application.dsource);
   qs.setSql("select * from books where isbn13=:isbn13");
   qs.addParam(name="isbn13",CFSQLTYPE="CF_SQL_NVARCHAR",value=arguments.isbn13);
   return qs.execute().getResult();
}
```

This searches the database for the book with the ISBN13 of whatever was submitted.

Now we need to call that function from our “view” layer (the mainForm function in addEdit.cfm)

<**cfset** thisBookDetails= addEditFunctions.bookDetails(book)>

This makes a variable called “thisBookDetails” and populates that variable with whatever it gets back from the “controller” which is the bookDetails function in the addEdit component.

Next let’s put the values from the database into the form. Adapt the title input tag to this:

```html
<input type=”text” name=”title” placeholder=”Book Title” value=”#thisBookDetails.title[1]#” />
```

The key difference is this **#thisBookDetails.title\[1]#**. The CF query object is a collection of structs and arrays. Each field is a key and it has an array of values. Therefore this notation references the variable thisBookDetails( which is the query that was returned ) , the field “title” and the first row of data. Make sense? Can you fill in the rest of the default values for the other text inputs?

The test is going to be when you submit the form. Does the data update in the DB? If not, check your code and try again.

Have fun!
