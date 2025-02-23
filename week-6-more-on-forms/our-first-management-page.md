---
hidden: true
---

# Our First Management Page

### Background

From reading the [Our Project And Its Users](../week-5-sql-and-modelling/our-project-and-its-users.md) document, it should be clear now that we are going to have two different areas of the site that we are creating. One is for the public and will be where most of the users of the site will browse and purchase books. The other is for the management of the bookstore and will be for the owners and employees of the bookstore and the bookstore website to perform administrative functions that will help the site (and company) run effectively and well.

Folder: /bookstore/management/

### Schema Check

All of you should have at least 4 SQL tables in your database. These are:

* Books
* Publishers
* People
* Roles

Do these tables still hold up since we’ve added the idea of having a management portion? They do. However, there are a few tweaks we need to do to our original design which stem either from mistakes in planning or from changed needs. These are listed below (along with the why)

#### Books Table

* Change the “language” field definition from nvarchar(20) to nvarchar(40). Some of the languages in the world are long. This can be done via the SQL Studio GUI interface by right clicking on the name of the table in the left panel and choosing DESIGN. It can also be done via an SQL statement which would be

alter table books alter column language nvarchar(40)

* Add a field called image which is a nvarchar(200)

#### Publishers

* Delete the ID column in the Publishers table and create a new column, also called ID. Make it an nvarchar(35). The reason we are doing this is that once you make a field an “identity” field, it might very difficult to change the data type. We haven’t gone too far down the process so we can just delete the column and remake it. However, have we already put the ID numbers into another table? Do we need to change those IDs with a new value?

## Primary Keys

In our four tables, we’ve discussed a few ways that we are going to make each row distinct. We discussed how a primary key was the main way that we were going to differentiate one row from another. We also discussed that a common method of determining a primary key was to use an auto numbered identity field. This automatically puts an integer into the field and counts up each time a row is created. I hinted at why, even though it is a common practice, there are some limitations to that practice, especially if we decide that we want to expand our database into mobile devices. The quick answer is that the numbers are assigned in order based on the database in which they are created. This means that number 100 which was created on one computer will not be the same record 100 that was created on another computer and now we have two records with the same id which could cause problems. Make sense so far?

With many of the new advancements in web and computer technology, it is possible for the same company or group to be entering data which is designed to be on the same database into many devices to be merged later. When the time comes to merge, we are now trying to put records together that all have the same ids, have relationships in their local databases that must be maintained in the master database. Identity fields are also not editable so if you do make a mistake, that number is gone forever in that database. Ugh!

So what’s the alternative? We are going to use something called a UUID which stands for Universally Unique Identifier. It is a 35 or 36 character code (32 characters with 3 or 4 dashes) which is generated a number of ways including based on the machine on which is made, the time, hashing, namespaces, randomness and others. It is technically possible for duplicates to be created but it is highly highly unlikely that there will be a collision. There are 3.4x1038 possible combinations so the change of repeated codes that will meet is slight.

UUIDs can be created automatically by many languages including ColdFusion using the function

\#createuuid()#

Very straightforward. Don’t forget to put it inside \<cfoutput>\</cfoutput> if it going to be visible on the page.

## Putting Queries into Web Pages

Last week we looked at how we can pass data from one page to another via a form. We also observed how we can use SQL to extract data from our databases. This week we are going to merge these two ideas and put some queries into our web pages.

### Practice Steps

1. Make folder called week 5 in your folder on the [comweb.uml.edu](http://comweb.uml.edu) website
2. Make two files
   1. query1.cfm which is a cfml file
   2. query1.cfc which is a Script Component

#### Creating query1.cfc

Query1.cfc is a component which means that it needs to contain this:\`

```
component {

}
```

We’re also going to start to cultivate some good habits in our coding and start putting in some “JavaDoc” notation to help clarify what this file does. Check the end of this document for more links about JavaDocs and documentation.

```
/***
 * Acts as the main controller for our practice query1.cfm page
 *
 * @author Dan Card
 * @date 2/13/2022
 **/
component {

}

```

The section at the top of the page in /\*\*\* \*\*/ helps to frame why this page exists.

#### Create our query function

We’re going to add a function to our component which will have 1 job and one job only. It will query our database for all the books in the db and return them.

\`

```
/**
 * Acts as the main controller for our practice query1.cfm page
 *
 * @author Dan Card 2/13/2022
 * @date 2/13/2022
 **/
component {

	/**
	 * Returns all the books in our database
	 *
	 **/
	function allBooks(){
		try {
			var qs = new query( datasource = "yourDataSourceName" );
			qs.setSql( "select * from books order by title" );
			return qs.execute().getResult();
		} catch ( any err ) {
			writeDump( err );
		}
	}

}
```

However, in order to check it, we need to have a “view” which will appear in the browser and display our data. Let’s turn our attention to the .cfm page.

#### Query1.cfm

The query1.cfm page should start with the same template with which you would start an html page.

```
<<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <cfset pageController=createObject("query1") />
    <cfdump var="#pageController.allBooks()#" />

</body>
</html>
```

1. Upload the page to the server and open it or start the CommandBox web server and open it locally.
2. Even if you have no books in your database you will see something like this:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dbbb4397-447d-48cf-9a96-eb9bb32e5bcb/Untitled.png)

1. If you do have books in your database, you will see a record of each one in the display.

Let’s look at the code:

| try {                             | try / catch is a standard technique in most languages which tells the code what to do if the code breaks. If it does, the server is supposed to run the code in the catch(){} code block which is discussed below.                                                                                                                                                                                                                                                                                                                                                             |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| var qs =                          | This creates a new variable named “qs”                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| new query( );                     | New is a keyword which creates a new “thing” in memory. In this case, the “thing” is a component called a “query” which is what makes the query call to the SQL server. We’ll look at how we see the results of that query below. In this respect, a query is another complex datatype that is unique to ColdFusion. Other languages have their own type of variable that handles query results. In that respect, the concept of having a variable with the query results in it is common across languages. However, the syntax used to access that data might not be uniform. |
| datasource = "yourDataSourceName" | The connection to the database is created beforehand and stored in the ColdFusion server itself. To access this connection we refer to it by name. Each of you has a datasource created which matches your blackboard username. If you followed the directions in the “Connecting your Local Development Environment to your UML Database” you saw how datasources are created.                                                                                                                                                                                                |

Sometimes this name is stored in the application scope. Remember that “scopes” are “buckets” of variables. We’ve looked at the URL, FORM and CGI scopes. The application scope is new. We will talk more about it later but for now know that each of you has your own ColdFusion application running, each with its own Application Scope. These variables are accessible from every page in your folder but are not accessible from outside your folder area. This prevents other people from putting data into your database by accident. | | qs.setSql( "select \* from books order by title" ); | We are telling the query component that this is the SQL query we want to run. It lists all the books in your books table and orders them by the title. By now, this statement should make sense. | | return qs.execute().getResult(); | This tell the CFML to execute the query and then to hand the results of the query back to whatever code called in. In this case, we mean our CFM page. | | catch ( any err ) { } | Every try{} needs to have a catch(){} block with it. This is the code to run if the code inside the try{} tag breaks or has an error. The error information is stored inside a variable called “err” in this case. | | writeDump( err ); | writeDump and its tag counterpart \<cfdump> are invaluable parts of debugging your code in CFML. No matter what the variable it, it will present it in a consistent and, many time, clear way. It will even try to tell you what line the error is on. |

Did all of that make sense? Did it work?

## Other Query Information

Along with the actual data from the query, you can see that there is some other information listed including the execution time (how long the query took to run), the SQL for the query and whether the query was cached or not. Caching is a process when the CF (or any server) saves something in memory so that it can serve it faster. This can be good for speed but not so good if the underlying data has changed. Usually, the process is pretty good a figuring out whether it should be cached or not but there are time where there are exceptions.

There are a number of other items which are available about this query. Some of them are listed below. I’ve used the name “allbooks” since that is what we just used but you would substitute “allbooks” for the name of the query you want to reference.

* **currentRow** - the number of the row the page is currently processing when it is outputting the query (i.e. 1,2,3,4 etc). When we loop over the query (as we will below) the currentRow is what row is currently being accessed
* **columnlist** – the list of columns in the query (this could be all of them if our SQL used the \* wildcard or it will match the columnist in our select statement).
* **recordcount** – the number of records which came back.

Copy and paste this under the query you made above:

_Allbooks has #allbooks.recordcount# books in it and the columns are #allbooks.columnlist#_

and you’ll see how it is displayed. Just some tidbits to file away for later.

### What To Do With A Query?

Once we have a query, what can we do with it? The two most common things to do with them are to use either \<CFOUTPUT query=””> or \<CFLOOP query=””>. We’ve already seen both of these tags but not in this context. More on this later.

### Our Project’s First Sketch

Our management page is going to look something like this:

![Figure 1: A rough sketch of our management page](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5548ebf2-2295-4415-9c0a-3d856d77d41e/Untitled.png)

Figure 1: A rough sketch of our management page

Just like it’s handy to have a diagram of the overall product, it helps to have a sketch of what page you are designing is going to look like, even if it is only a rough idea. Since this is the management page, there is less an emphasis on fancy visual design (although it doesn’t have to be completely Spartan).

On the left will be a list of the books in the database. We will start with a list and then make it searchable as the list of books gets longer. In the main area, we’ll have a form which has the inputs needed to manage the book data. This doc as written will be easier to debug if there are at least one or two books in your books table already but that isnt necessary. You can put data into your table via SQL Management studio or whatever tool you are using.

### Creating the basic structure of the page – index.cfm.

The page is going to have two columns and we will use Bootstrap to do the main layout.

1. In your “MyFinalProject” folder, create a folder called “MANAGEMENT”. We are going to create the index page for your management area.
2. Create a file called index.cfm using the basic format as we’ve already looked at in this class including the links to Bootstrap:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link href="<https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css>" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
    <script src="<https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js>" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>
</head>
<body>

</body>
</html>

```

1. In the body tag, put in a div with the class of container \<div class=”container”> \</div>
2. In the div.container, put 2 additional divs with the ids of “navarea” and “mainarea”.
3. In the div#mainarea put \<cfinclude template=”#tool#.cfm”>. We’re going to use “tool” as the parameter to determine which module we are going to load into our page. This is similar to how we used the variable “p” in the LearnCF exercises.
4. Whenever you are going to display a variable on your page, you need to make sure that the variable has been created. Otherwise you get an error. In this case, we are going to ensure that the “tool” variable always exists by using the \<cfparam> tag. Put this: \<cfparam name=”tool” default=”addedit”> above the body tag. What this tag does is search many of the other scopes (i.e. FORM, URL, SESSION, APPLICATION etc. If you’re really interested, [here is a link](https://helpx.adobe.com/coldfusion/developing-applications/the-cfml-programming-language/using-coldfusion-variables/about-scopes.html) to the different scopes that are available as of CF 2021) and, if it doesn’t find a variable with that name, creates one (in the VARIABLES scope) and gives it the default value.

Here is what you should have so far:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link href="<https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css>" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
    <script src="<https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js>" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>
</head>
<body>
    <cfparam name="tool" default="addEdit" />

    <div id="wrapper" class="container">
        <div id="navarea"></div>
        <div id="mainarea">
            <cfinclude template="#tool#.cfm" />
        </div>
    </div>
</body>
</html>
```

### Creating our First Module – addedit

As we saw in the previous section, we have an index page and then a place for modules (other collections of code that perform a function) to go. We’re going to create our first one which will be the primary tool we use to add and edit books in our bookstore. We are also going to start separating out our “view” from things that are purely “functional” or non-presentational. First let’s create where we are going to put our controller code.

Create two new files in /myfinalproject/managment called addedit.cfm and addedit.cfc

Now, let’s start to create our “view” code:

#### AddEdit.cfm

Create a file called “addedit.cfm” which is a blank page (no HTML or tags in it). Put in this structure:

```
<cftry>
    <cfset addEditFunctions = createObject("addedit") />
    <div class="row">
        <div id="main" class="col-9">
            Main Area
        </div>

        <div id=”leftgutter” class="col-lg-3 order-first">
            Left side
        </div>
    </div>
    <cfcatch type="any">
        <cfoutput>
            #cfcatch.Message#
        </cfoutput>
    </cfcatch>
</cftry>

```

The \<CFTRY> and \<CFCATCH> tags are important. If there is a problem with your ColdFusion……check that…..WHEN there is a problem with your ColdFusion code, since no one ever does everything 100% correctly the first, or perhaps even the fiftieth time, the error doesn’t always display on the screen so debugging can be very difficult. The \<CFTRY> and \<CFCATCH> tells the system what to do when there is an error. In this case, display the error message.

The “\<cfset addEditFunctions = createObject("addedit") >” tag links your view to your controller or more simply put, tells your page where to access some functions it’s going to need. Notice how there is no extension on the “addedit”. When you are creating a CFC like this, it is assumed that is going to be a .CFC file.

View your index page in the browser either locally or upload it and see it on the class server. Did you get an error? Why? What do you have to add to make the page work so far?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5cb5f77f-076d-45b8-9d41-a53fc361ed10/Untitled.png)

There are three elements to addEdit.cfm

1. The form where you input the book details
2. The function that processes the book details and puts them into the system
3. A side navigation that will allow the user to select the book they wish to edit which will populate the form with that book’s details.

Each of these will have their own function to help us keep the code organized.

At the bottom of the page, add two functions called sideNav and mainForm. Put a function call in the appropriate places in the page. Your page should now look like this:

```
<cftry>
    <cfset addEditFunctions = createObject("addedit") />
    <div class="row">
        <div id="main" class="col-9">
            <cfoutput> #mainForm()#</cfoutput>
        </div>

        <div id=”leftgutter” class="col-lg-3 order-first">
            <cfoutput> #sideNav()#</cfoutput>
        </div>
    </div>
    <cfcatch type="any">
        <cfoutput>
            #cfcatch.Message#
        </cfoutput>
    </cfcatch>
</cftry>

<cffunction name="mainForm">
    Main Form
</cffunction>

<cffunction name="sideNav">
    Side Nav
</cffunction>
```

From now on, most of the work we do will be focused on one of these functions.

For the rest of the exercise we are going to do three things

1. Create a very simple form which will have two inputs.
2. Create the function to add new books to the database
3. Create a side navigation to see the books in the database.

## Creating the Editing Form

Forms are very handy things. They can also be very complicated things with a lot of moving parts. We are first going to create a simple form and submit it. Then we are going to expand. Forms are used to pass data from one page to another in a different format than passing them through a URL. You wouldn’t want your password to be visible in the URL where any passerby can see it, would you? Or anyone accessing your history? Probably not. Forms also allow us to submit different types of information whether it’s a simple string, long paragraphs, even files or pictures. Inside forms, there are several tags which we will use here. These include:

* \<input>
  * Type=”text”
  * Type=”hidden”
  * Type=”checkbox”
  * Type=”radio”
* \<textarea>
* \<select>
* \<button>

Let’s get started. Again, we’ll walk through the steps. After each step, check your page and make sure it’s working like you expect before going on to the next step.

Here is the beginning of our mainForm function:

```
<cffunction name="mainForm">
    <cfoutput>
        <form action="#cgi.script_name#?tool=addedit" method="post">
            <label for="isbn13">ISBN13:</label>
            <input type="text" id="isbn13" name="isbn13" value="" placeholder="ISBN13" />
        </form>
    </cfoutput>
</cffunction>
```

| Line of Code                             | Explanation                                                                                                                                                                                                                                                        |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| \<cfoutput>                              | There are variables in the of the form so it needs to be wrapped in \<CFOUTPUT>                                                                                                                                                                                    |
| \<form                                   | All forms need a form tag                                                                                                                                                                                                                                          |
| action=”#cgi.script\_name#?tool=addedit” | We saw last week how the “action” the page that the form takes the user when it is submitted. We are going to have it open this page again.                                                                                                                        |
| method=”post”>                           | There are several methods which a form can use. The two most popular are GET, where the variables and values are put in the URL string and POST which is when they are submitted “behind the scenes”. We’re almost without exception going to use POST with forms. |
| \<label for="isbn13">ISBN13:\</label>    | The label tag has some built in formatting with Bootstrap. The \<label> tag also helps with accessibility readers. If you match the “for” attribute to the “id” of the input, it links the two in both the reader and in the browser.                              |
| \<input type=”text” id=”isbn13”          | There are many types of inputs. Text is the most basic. It is simply a text box which can accept an input.                                                                                                                                                         |
| name=”isbn13”                            | This corresponds with the name of the variable in the FORM scope on the action page.                                                                                                                                                                               |
| placeholder=”ISBN13” />                  | The placeholder attribute establishes what is displayed when the input box is empty.                                                                                                                                                                               |
| \</form>                                 | The tag for the form                                                                                                                                                                                                                                               |
| \</cfoutput>                             | Closes the \<cfoutput> tag                                                                                                                                                                                                                                         |

Add another input for the book title:

```html
<label for=”title”>Book Title</label> <input type=”text” id=”title” name=”title” placeholder=”Book Title” />  
```

Do you know where this line of code goes? Probably but just in case, it would go after the isbn13 input and before the \</cfoutput> tag.

At the bottom of the form add a submit button by adding

```html
<button type=”submit” class="btn btn-primary">Add Book</button>  
```

Buttons inside a form default to submitting the form when clicked. If we don’t want that, we need to establish the button as a button in the “type” attribute (type=”button”). The class, “btn btn-primary” are two classes in Bootstrap we can use to round the corners, color the background of the button and add a highlight when the user rolls over the button.

Your form will now submit. Click on it! Impressive huh? HUH? HUH? Jk. You probably didn’t see anything happen. Your page looks just like it did before, doesn’t it? Because although we have passed in the variables we haven’t done anything to “catch” them yet. A lot of programming is passing values from one thing to another to do their magic and you need to make sure you have both sides of the equation – a “passer” and a “receiver”

Open the page in your browser. It should look like this:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6715d518-6bbe-4736-858f-c015778774b3/Untitled.png)

### Processing the Form Submission

Where are we processing the data the form passes to the page? There will be no visible elements in that function that will be directly displayed on the screen. Therefore, it doesn’t go in the view layer. We’re going to put that in our addEdit.cfc file in a function called processForms() function.

Notice that we created this file a bit differently. It is not using the CML tag syntax. We’re going to write our CFCs using the CFML script syntax which looks more like some other languages like Javascript and Java.

In the processForms function, we are going to write the code to handle the form submission. This includes doing any processing or manipulating of the data before it gets entered into the database and then either inserting or updating the data. First, let’s look at what’s being passed to the page.

At the top of the addedit.cfm page, function, add \<cfdump var=”#form#”> and then put some values into the form and submit it. Any “Post” data from a form (remember we said ‘method=”POST”’) is stored in the “form” variable scope (remember, a scope is just a bucket that holds variables). It always exists so we can always dump it out without risk of it being defined or not. Same with URL and some other scopes. Here is what we get from submitting our form:

We can see from the dump that there are two variables being passed in: title and ISBN13 which is what we would expect. Let’s pass all of that form data to our processForm.

Add this line to top of our addEdit.cfm:

```html
<cfset addEditFunctions.processForms(form)>
```

Technically, we don’t HAVE to do this because the CFC would be able to access the form scope directly but we’re going to do it this way for reasons we will discuss later in the class.

Open addEdit.cfc and add the processForms function. It looks like this:

```html
function processForms( required struct formData ){

} 
```

First we need to receive the data which our CFM page is passing to us. This is done with the formData argument in the parenthesis An argument is data the function needs to run properly. In this case, we’re going to call it formData. It is going to be struct and it is going to be required. If the function doesn’t receive any data or receives data that is not a struct, it will throw an error.

```html
function processForms( required struct formData ){
    writedump( formData );  
}
```

if we were going to write this in the tag syntax it would look like this:

```html
<cffunction name=”processForms”>
    <cfargument name=”formData” type=”struct” required=”true”>
    <cfdump var=”#formData#”>
</cffunction>
```

Which is more readable and concise?

In processForms, we’re going to write the code to add this data into our db, but we don’t want the code to run every time the page opens, only when we actually submit the form. We can do this with an if() statement. We looked at how to do that in the tag format with

\<cfif>…..\</cfif>

In script it looks like this:

```html
if( some expression which is true or false  ){
    Stuff to do if it is true
}
```

Change your function to looks like this:

```html
function processForms( required struct formData ){      
    if( formData.keyExists(“isbn13”) ){            
		    writedump( formData );
    }  
}
```

The keyExists() method checks and sees if a struct has a particular key. If it does, it comes back with true. If the structure does not have a key with that name, it comes back false. In this case, it checks to see if the variable formData has a key named “isbn13”. If so, it will dump out formData. Now the form variables will only dump out if and when we submit the form. Open the page without submitting the form and then after submitting it. Does that work as expected?

Now, let’s insert the data we submit.

The keyword for putting the data into the DB is INSERT. Let’s write the SQL and output it on the screen. We won’t run it yet, just get the SQL correct.

```html
writeoutput(“INSERT into BOOKS (isbn13,title) VALUES (‘#form.isbn13#’,’#form.title#’)”);  
```

Let’s walk through that:

| Code                                     | Description                                                                                                                                                                                                                                   |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Writeoutput()                            | This is the script format to tell CF to display what is in the () on the screen                                                                                                                                                               |
| INSERT                                   | The keyword signifying that we are  putting data into the DB                                                                                                                                                                                  |
| Books                                    | The table into which we are putting the data                                                                                                                                                                                                  |
| (isbn13,title)                           | The list of fields into which we are putting the data. IMPORTANT: All the values in this list need to match up with a field in your database.                                                                                                 |
| VALUES                                   | The keyword signifying that the values to insert are next                                                                                                                                                                                     |
| (‘#formData.isbn13#’,’#formData.title#’) | The values are dynamic and are coming from the submitted FORM scope. CF will substitute in these values for the submitted ones. IMPORTANT: All the names of the variables (formData.XXXX) need to match up with a name property on your form. |

Your page with the submitted form might look like this:

First we create a query object: var qs = new query( datasource = application.dsource );

| Code                             | Description                                                                                                          |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| var                              | This establishes a variable                                                                                          |
| qs                               | This is the name of the variable we’re creating.                                                                     |
| new                              | This is a key word saying that we are creating a new object                                                          |
| query()                          | This is a function that creates a query object. An object is a collection of code that might do something.           |
| Datasource = application.dsource | We are telling the new query object that it should use the datasource that matches the variable application.dsource. |

The next line is qs.setSql(“insert into books (isbn13,title) values (:isbn13,:title)”);

| Code           | Description                                                                                      |
| -------------- | ------------------------------------------------------------------------------------------------ |
| qs             | This is the query object                                                                         |
| setSQl(“”)     | This sets the SQl for the query                                                                  |
| :isbn13,:title | These are placeholders in the query. We are going to add some extra protections for our database |

qs.addParam(name=”isbn13”,cfsqltype=”CF\_SQL\_NVARCHAR”,value=formData.isbn13);

This is new syntax. This line puts in some safeguards that help protect the database from malicious SQL.

| Code           | Description                                                                       |
| -------------- | --------------------------------------------------------------------------------- |
| qs             | The query object                                                                  |
| qs..addParam() | A function that adds a cfqueryparam to the query                                  |
| Name=”isbn13”  | The name of the parameter. It corresponds to the placeholder in the previous line |
| cfsqltype      | This checks to make sure that data it is submitting is the correct type           |
| value          | The value to be submitted to the database                                         |

qs.addParam(name=”title”,cfsqltype=”CF\_SQL\_NVARCHAR”,value=formData.title);

execute() Run the actual query

Submit the form. Did you get any errors? Check the database. Was the item added?

If it didn’t add, go through the code and figure out why.

Here is the whole function:

```
function processForms( required struct formData ){
   if ( formData.keyExists( "isbn13" ) ) {
      var qs = new query( datasource = application.dsource );
      qs.setSql( "insert into books (isbn13,title) values (:isbn13,:title)" );
      qs.addParam(
         name      = "isbn13",
         cfsqltype = "CF_SQL_NVARCHAR",
         value     = formData.isbn13
      );
      qs.addParam(
         name      = "title",
         cfsqltype = "CF_SQL_NVARCHAR",
         value     = formData.title
      );
      qs.execute();
   }
}
```

## Creating the Side Book Selection System

1. We are going to create a query to retrieve the data we’re going to show in the side nav. The query should be in the controller layer because it is not going to directly be shown on the screen – it’s logic, not presentation. In the sideNav function in addEdit.cfm, add this line: \<cfset allbooks = addEditFunctions.sideNavBooks()> Using the processForms function as a model, can you create a “sideNavBooks” function in the addEdit.cfc file that gets all the books from the books table? The SQL is “select \* from books”.
2. Inside the sidenav function we are going to use a \<ul> tag to create the list of books on the left hand side.

```
<cffunction name="sideNav">
    <div>
        Book List
    </div>
    <cfoutput>
        <ul class="nav flex-column">
        <cfloop query="allbooks">
            <li class=”nav-item”>
                <a class=”nav-link”>#trim(title)#</a>
            </li>
        </cfloop>
        </ul>
    </cfoutput>
</cffunction>
```

See what’s going on there? Let’s walk through it.

| Code                                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| \<div>                                  | The side bar needs something to give it some context. This div will act as a label for the panel so our users don’t forget what it is.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Book List                               | The label                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| \</div>                                 | The end of the div element.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| \<cfoutput>                             | We’re going to need ColdFusion to display some variables in this area so we wrap it in \<cfoutput> tags.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| \<ul class="nav flex-column">           | The list of books is just that, a list. We’ll use the Bootstrap classes nav and flex-column to give it some style.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| \<cfloop query="allbooks">              | Now, we’re getting into the actual display of the content from the database. CFLOOP is the tag for ColdFusion to perform…well….a loop. A loop is basically when we tell the program to “do everything inside this block until something tells you to stop”. There are many triggers that will tell the loop to stop and we’ll look at many of them over the next few weeks. In this particular instance, it will loop over the query until it has looked at every record and then it will go on with the rest of the page. In this case, it will loop over the query “allbooks”. Quick Note: there are no #s around the name of the query. It is the name of the query only. |
| \<li class=”nav-item”>                  | This is the tag for a list item. Each book is its own list item.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| \<a class=”nav-link”>#trim(title)#\</a> | This is where the heart of the matter is. When we finish this list next week, each of these items will be a link that will tell the module to retrieve the information about a particular book. For the time being, the #trim(title)# will display the title of the book. The trim() function removes any spaces that might have made their way into the system by accident.                                                                                                                                                                                                                                                                                                 |

Notice that there is no href attribute yet. This link won’t go anywhere as it. | | \</li> | The end of the List Item |

When you submit a new book, the new book title should appear in the side nav listing immediately. If it doesn’t, you might be missing a step.

Did it work? Have fun!

## More Reading

[https://docbox.ortusbooks.com/getting-started/annotating-your-code](https://docbox.ortusbooks.com/getting-started/annotating-your-code)

[https://www.oracle.com/java/technologies/javase/javadoc-tool.html](https://www.oracle.com/java/technologies/javase/javadoc-tool.html)
