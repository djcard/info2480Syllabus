# Adding WYSIWYG to the Manage Books Tool

## Background

We are going to add a new field to our manage books tool ( addEdit.bxm ) which is going to allow us to write a description of the book so our customers can see if they want to buy it or not. The basic steps are

1. Adding a field to our books table
2. Adding the control to our manage books form and adding CKEDITOR to that as well.&#x20;
3. Adapting our queries to accomodate the new field.&#x20;
4. Adapting our details.bxm page to display our new description.&#x20;

## Adding a Description Field to the Books Table

1. Open MySQL Workbench and connect to your database
2. Right click on your books table and choose Alter
3. Add description bottom of the list of columns and make it a nvarchar(1000) (Why this data type?)
4. Press Apply and then Apply to save the table.

## Editing your Add/Edit Form

We are going to use a new form element called a \<textarea> as the basis of our WYSIWIG area. Add the following code to your add/edit form:

```
<div class="form-floating mb-3">
    <textarea id="description" name="description" class="form-control" >
        <cfoutput>#thisBookDetails.description#</cfoutput>
    </textarea>
    <script>CKEDITOR.replace('description');</script>
</div>
```

The first \<div> wraps the \<label> and the \<textarea> and should include all the css classes that will stylize your form, either according to the bootstrap rules as described in other docs or by your own styling. The textarea has a start tag and an end tag. In between is the value we want by default. In this case, it is the value #trim(thisBookDetails.description\[1])# which is the description field from the first row of the query bookinfo.

The \<script> tag is what converts the text area to the WYSIWYG tool. It calls an object called CKEDITOR which is created in the script “ckeditor.js” to which we linked in the first step above. It calls a function (a preset series of commands) called “replace” and tells the function to replace the element with the id of ‘description’.

Upload your addedit.cfm page. Does the WYSIWYG show up?

## Adapting the Update Query

In the ProcessForms function on the addedit.cfm page is the query which updates the database. We need to add the description field to this update. Somewhere in the query add after the SET keyword and before the WHERE keyword add:

Description = :description

Make sure you add commas where needed to make the query work correctly. Also add the parameter

qs.addParam(name=”description”,value=formData.description);

Upload your addedit.cfm and addEdit.cfc page. Try the “round trip” process. Load the page, choose a book, add a description and save. It. Did it save?

## Adapting the Details.cfm Page

We need to adapt the details page in the public facing area of the website to show the description. In the details page, add

\<span>Description: #bookinfo.description\[1]#\</span>

to the book details area. Save and upload details.cfm.

Did it display correctly? Go back and edit the description and use the controls to add some more HTML including links, bold, italicized etc. Save it and look at the details page again. Did it work?
