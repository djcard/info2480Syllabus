# Adding to our Management Tool

## Background

It’s been said that you can’t judge a book by its cover. This is especially true if you have no idea what the cover looks like. So far, in our database, we have some information about our books but it’s all text. There are no graphics and most bookstore have images. Lots of images. Book jackets are designed to catch your eye. You might not judge a book by its cover, but the book publishers sure want to make sure you have the opportunity to do so.

It stands to reason that we would want to display the book jacket along with the book information. Since we want to manage our books via the web, we probably need to figure out how to upload an image, save it, attach the image to our book record and display it on demand.

To do that we are going to look at a new input type \<input type=”file”> and a built-in CF function called fileUpload().

We also have three data tables that we have not touched as of yet: Publishers, People and Roles.

Ok, you convinced me. We’ll do it. It is going to take four steps which are:

1. Make some schema changes
2. Populate some data
3. Edit our book form
4. Edit our update queries

## Editing our Schema

We need to make some changes in our schema to make these items work. For one, we need to add a field to contain the image information. We also have a few type mismatches that we need to clear up.

Open your SQL management tool (SQL Studio or other program) and make the following changes to the schema for your project. You can do this either using the GUI or using the SQL keyword ALTER. If you aren’t sure how to do that, can you do an Internet search to find the syntax?

1. In the people table, change the id field from an int to nvarchar(35). You might need to delete the field make a new field called id.
2. In the publisher table, change the id field to a nvarchar(35). Same here.

## Populating Data

In the people table, we originally had the id as an int with the identity property set to true. This made the id an integer (obviously) that was set automatically whenever a new record is created by simply adding the next number. Many of you looked at and asked if it was going to cause a problem if the id field in the publisher table was an integer and publisher property in books was a string. The answer then was “just wait” but the actual answer it “Yes” it will. I wanted you to learn how to create an identity field since it is a common technique in database creation.

However, we’re not going to use an automatically created integer as the primary key on the table. Instead, we are going to use a UUID which stands for Universally Unique ID. This is a little bit of a misnomer since there is no guarantee that it is universally unique. Here is the write up from Wikipedia about UUIDs:

> The number of possible UUIDs is 340,282,366,920,938,463,463,374,607,431,768,211,456 (16^32 or 2^128), or about 3.4 × 10^38. For comparison there are an estimated 10^80 atoms in the observable universe. In [Short Scale](http://en.wikipedia.org/wiki/Long\_and\_short\_scales), it would be read as: "Three hundred forty undecillion, two hundred eighty two decillion, three hundred sixty six nonillion, nine hundred twenty octillion, nine hundred thirty eight septillion, four hundred sixty three sextillion, four hundred sixty three quintillion, three hundred seventy four quadrillion, six hundred seven trillion, four hundred thirty one billion, seven hundred sixty eight million, two hundred eleven thousand, four hundred fifty six."

Given that number of possibilities, the chances that the same value will appear in the same collection of data is very very very small. The reason I want to focus on using UUIDs is that more and more, data is being created across multiple devices and multiple computers. If all of the ids created are auto numbered, it is almost a certainty that multiple records will have the same identity numbers for different data across all of these databases. This makes it more difficult to merge data and keep relationships clean while doing so. A UUID makes it a bit easier to do that.

UUIDs are created based on a number of factors including the type of computer on which is creating it, the MAC address of the network card, the time the uuid was created and a few other aspects. Many programming languages have functions that will create uuids for you. CF is no exception. Currently, we have one table, people, which either has dummy data in the id field or is blank. We need to replace those with UUIDs. The publisher table has the same problem in that its ID field either has dummy data in it or is blank. We need to put uuids in those fields. We are going to use \<cfloop> to create a number of uuids so we can copy and paste them into the db or into the SQL we use to update the db. UUID is often used interchangeable with GUID which stands for Globally Unique ID.

### To create UUIDs:

1. In the /myFinalProject/management/ folder, create a file in that folder called createuuids.cfm
2. In createuuids.cfm , type the following:

```html
<ul> 
		<cfoutput> 
				<cfloop from=”1” to=”20” index=”I”> 
						<li>#createuuid()#</li> 
				</cfloop> 
		</cfoutput> 
</ul>
```

Save and open the page and you will something similar to this:

* 05B67055-D1C6-74F8-4AB5D7525084909F
* 05B67056-E68F-6344-E40F9375A74B6124
* 05B67057-CC92-157E-B87CBD98EA766C5B
* 05B67058-C1CE-C138-9D68C86F78672000
* 05B67059-AC75-E474-7205F46BF1DE33CC
* 05B6705A-DD69-D629-88C45FE9851D1268
* 05B6705B-CE51-57DF-A1DB21EBC261F167
* 05B6705C-D5E0-0CCC-D7F481CCB3EBA3D4
* 05B6705D-CFD8-4C3E-F73809D4F54471BB
* 05B6705E-FE62-71AA-7FC557A5746B848E
* 05B6705F-C245-8E5B-9F086D935A1DEBFE
* 05B67060-CB4C-235F-7EA08E59B4379DBB
* 05B67061-F55E-B022-020AD65D481EA7D1
* 05B67062-FB9A-09BD-A2C17D76643D0F44
* 05B67063-EC7E-577A-E3C8222F73531072
* 05B67064-FCBE-751F-8DF2A3AD4EC2A36A
* 05B67065-0BB6-CFFF-D06B0A69E466D9B1
* 05B67066-D628-B6C5-90ED095D9997B8A7
* 05B67067-C36C-BD6B-258071C2AEBAF943
* 05B67068-A4B2-357E-B8AD6DCF94C12B25

Add an item to the navigation in your management area to open this module when you need it.

Use these values (not the ones in this document, the ones you create) to update the id columns in the people and the publisher tables.

Make the id columns in the publisher table and the people table to be primary ids.

## Adding a Folder

In your myFinalProject folder, add a folder called “images”. Make sure you don’t just create it on your local machine, upload it or create it on the server as well.

## Editing Our Form

There are two more elements we need to add to our management form located in /MyWebSite/management/addedit.cfm (this is the first management page which we created). This form should be in the function mainForm at the bottom of the page, correct?

### Adding the Publisher Input

The publisher input is going to be a type of input called a “select” tag. It’s also called a “drop down” and I’m sure a few other things. A \<select> has a name just like the other form inputs we’ve looked at. This is the key used in the FORM scope when the form it submitted. Within the \<select> and \</select> are a series of \<option> tags which define, you guessed it, the options that available in the select tag. Here is a simple select tag:

```html
<select name=”publisher”>         
		<option value=””></option> 
</select>
```

This select has one option which is blank. This is a typical setup for a select since there is usually a blank option at the top, so it appears blank. This makes it clear that a value has not been chosen. We are going to use a query to get all the publishers in our database and make options from the data we get back. We are also going to make it so that the correct publisher is selected if one has been set.

1. In addEdit.cfc create a new function which will be allPublishers. Can you do this by using the other functions in the component as an example? Check out the CodeBase examples if you need to.
2. Add a call to the allPublishers function from addEdit.cfm at the top of the mainForm function like this:

<**cfset** allPublishers = addEditFunctions.allPublishers()>

Use the results of this query to make the other options in our select:

```
<div class="form-floating mb-3">
    <select class="form-select" id="publisher" **name="publisher"** aria-label="Publisher Select Control">
        <option ></option>
        <cfloop query="allPublishers">
            <option value="#id#">#name#</option>
        </cfloop>
    </select>
    <label for="publisher">Publisher</label>
</div>
```

**Don’t forget to add the NAME attribute to the select control.**

A \<select> tag can have only one of its options selected at a time. The selected options value is the value passed when the form is submitted. We are using the id (which should now be populated with UUIDs) as the value being passed. We don’t want to see the UUID when we open the menu, we want to see the name of the publisher. Therefore, we are putting the NAME field between the \<option> and \</option> tags. This is what appears in the dropdown.

Save the file and upload it. Did it work?

We still need to make it so that the correct option is selected when one has been chosen. In order to make that happen we need to set the SELECTED attribute of the option where the ID in the PUBLISHER table is equal to the PUBLISHER field in the BOOKS table. Can you think of how we can make that happen? We need to find a way to drop the word “selected” as an attribute in the option tag If the ID is equal to the PUBLISHER field in books.

We’re going to use something called a “Ternary Condition”. This is a short hand way of doing an “if-else” statement which makes for very clean, concise and readable code. Add the bolded text below to the \<option> tags in the publisher drop down.

`<option value="#id#" **#id eq thisBookDetails.publisher ? "selected" : ""#** >#name#</option>`

Let’s unpack that

| Code                            | Description      |
| ------------------------------- | ---------------- |
| id eq thisBookDetails.publisher | This is the “IF” |

“id” is the value from the publishers table. thisBookDetails.publisher is the publisher field from the query about the book we are editing.

eq is the CFML syntax for “is equal to”. Note a few things

1. a single “=” assigns a value as in var x=5. Two equals “==” is comparing two values.
2. CFML on the Lucee server ( and other scripting languages in general ) can use two “==” to compare two values. However, in the tag syntax, Adobe ColdFusion still uses only the eq syntax for a comparison.
3. JS also uses “===” but CFML does not. Any idea why not? | | ? “selected | If the “IF” part is true, this is the value2 | | : “” | If the “IF” part is false, this is the value |

Try this. You will need to populate some rows in your publisher table.

### Editing the update query

This is straightforward. Simply add to the update phrase in the processForms function and add the necessary queryparam.

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
             pages=:pages,
             **publisher=:publisher**
         WHERE isbn13=:isbn13
      ");
      qs.addparam(name="isbn13",cfqsltype="CF_SQL_NVARCHAR",value=formData.isbn13,null=formData.isbn13.len()!=13 );
      qs.addparam(name="title",cfqsltype="CF_SQL_NVARCHAR",value=formData.title,null=formData.title.len()==0 );
      qs.addParam(name="weight",CFSQLTYPE="CF_SQL_NUMERIC",value=formData.weight);
      qs.addParam(name="year",CFSQLTYPE="CF_SQL_NUMERIC",value=formData.year);
      qs.addParam(name="pages",CFSQLTYPE="CF_SQL_NUMERIC",value=formData.pages);
      **qs.addParam(name="publisher",CFSQLTYPE="CF_SQL_NVARCHAR",value=formData.publisher);**
      qs.execute();
   }
}
```

## Adding Images

This process is a little more elaborate.

1. We need to add 2 elements to our form.

\<input type=”file” name=”uploadimage”> \<input type=”hidden” name=”image” value=”#trim(thisbook.image\[1])#”>

```
<label for="uploadImage">Upload Cover</label>
<div class="input-group mb-3">
    <input type="file" id="uploadImage" name="uploadimage" class="form-control" />
    <input type="hidden" name="image" value="#trim(thisBookDetails.image[1])#" />
</div>
```

Why two? What are each of these tags going to accomplish?

We also need to make one more changes to our form tag.

1. add **enctype="multipart/form-data"** so it reads: \<form action="#cgi.SCRIPT\_NAME#?book=#url.book#" method="post" enctype="multipart/form-data" > This is because, while text boxes send information in plain text, images are stored as Binary objects and the form needs to be able to send both text and binary objects.
2. Because we have made this page a module which fits into a larger index.cfm, we also need to pass in what tool we are using. The action attribute, therefore, needs to change to reflect that.

\<form action="#cgi.SCRIPT\_NAME#?tool=#tool#\&book=#url.book#" method="post" enctype="multipart/form-data" >

`<form action="#cgi.script_name#?tool=addEdit&book=#book#" method="POST" enctype="multipart/form-data" >`

## Editing our Update Query

At the top of our processForms function on the addEdit.cfc page, we have a block of code which starts with

**if**

(formData.KeyExists(

**"isbn13"**

)){

This checks to see if we have submitted the main form and whether it should update the database or not. Inside that if(){} block, we are going to add another one. This is:

**if**

(formData.keyExists(

**"uploadImage"**

)

**and**

formData.uploadImage

**neq**

**''**

){

formData.image = uploadBookCover();

}

This will check to see if an image has been uploaded. If it has, we need to have the system do a little bit of work first. As you can probably tell by now, this is going to call another function called uploadBookCover. This is going to go in our addEdit.cfc component as well.

```
function uploadBookCover(){
   var imageData = fileUpload(expandPath("../images/"),"uploadImage","*","makeUnique");
   return imageData.serverFile;
}
```

FileUpload takes 4 arguments. Arguments are data that are passed to a function in order for the function to run. In this case the four arguments are

1. Destination (The folder where the image will be sent) expandpath(**'/'**) & **/CodeBase/images/"**
2. fileField – The form field with the image data - **"uploadimage"**
3. accept – the types of images the upload will accept - **"\*"**
4. nameconflict – What should the upload do if there is already a file with that name in the destination folder. - **"makeunique"**

FileUpload also returns a structure which contains information about the file which was uploaded. If we dump out imageData using writedump(imageData);  We see this:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9166e421-918d-4172-8a07-7d7602b44720/Untitled.png)

There are a number of items here but the two we are particularly interested in are the SERVERDIRECTORY and SERVERFILE properties. The SERVERDIRECTORY is the folder to which the image was uploaded. The SERVERFILE is the name of the image we just uploaded. If there had already been a file with that name, the server would have given it a unique name because we set nameconflict=”makeunique”. We could have set it to “overwrite” in which case it would have overwritten the file.

Now going back to our processForms function, we set

formData.image = uploadBookCover()

and we are returning the name of the image from uploadBookCover. Therefore, our query (once we adapt it) will simply write the name of the image into the database.

In our form, we added two \<input> tags – one with the type =”file” with name=“uploadimage” and the other type=”hidden” and name=”image”. Why two? Hopefully now you see that one (image) was to hold the value of the image that was already in the database. The other (uploadimage) was in case we wanted to upload a different file. If we do upload a new image, we process the upload, get the name of the new file and put it into the formData.image variable.

We now need to add the new fields to our query. Your processForms function should look something like this:

```
function processForms( required struct formData ){

   if ( formData.keyExists( "isbn13" ) && formData.isbn13.len()==13 && formData.title.len() > 0) {

      if(formData.keyExists("uploadImage") && formData.uploadImage.len() > 0){
         formData.image = uploadBookCover();
      }

      var qs = new query(datasource=application.dsource);
      qs.setSQL("
      IF NOT EXISTS( SELECT * FROM books WHERE isbn13=:isbn13)
              INSERT INTO books (isbn13,title) VALUES (:isbn13,:title);
      UPDATE books SET
             title=:title,
             weight=:weight,
             year=:year,
             pages=:pages,
             publisher=:publisher,
             image=:image
         WHERE isbn13=:isbn13
      ");
      qs.addparam(name="isbn13",cfqsltype="CF_SQL_NVARCHAR",value=formData.isbn13,null=formData.isbn13.len()!=13 );
      qs.addparam(name="title",cfqsltype="CF_SQL_NVARCHAR",value=formData.title,null=formData.title.len()==0 );
      qs.addParam(name="weight",CFSQLTYPE="CF_SQL_NUMERIC",value=formData.weight);
      qs.addParam(name="year",CFSQLTYPE="CF_SQL_NUMERIC",value=formData.year);
      qs.addParam(name="pages",CFSQLTYPE="CF_SQL_NUMERIC",value=formData.pages);
      qs.addParam(name="publisher",CFSQLTYPE="CF_SQL_NVARCHAR",value=formData.publisher);
      qs.addParam(name="image",CFSQLTYPE="CF_SQL_NVARCHAR",value=formData.image);
      qs.execute();
   }
}
```

Done?

In our form, let’s show the image that is already in the database and also the file name.

Here is one way we can do that:

```
<div class="row">
    <div class="col">
        <label for="uploadImage">Upload Cover</label>
        <div class="input-group mb-3">
            <input type="file" id="uploadImage" name="uploadimage" class="form-control" />
            <input type="hidden" name="image" value="#trim(thisBookDetails.image[1])#" />
        </div>
    </div>
    <div class="col">
        <cfif thisBookDetails.image[1].len() gt 0 >
            <img src="../images/#trim(thisBookDetails.image[1])#" style="width:200px" />
        </cfif>
    </div>
</div>
```

Done with this one! How’d you do?
