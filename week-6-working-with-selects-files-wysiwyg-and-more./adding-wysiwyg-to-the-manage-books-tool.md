# Adding WYSIWYG to the Manage Books Tool

## Background

We are going to add a new field to our manage books tool ( addEdit.bxm ) which is going to allow us to write a description of the book so our customers can see if they want to buy it or not. The basic steps are

1. Adding a field to our books table
2. Adding the control to our manage books form and adding CKEDITOR to that as well.&#x20;
3. Adapting our queries to accommodate the new field.&#x20;
4. Adapting our details.bxm page to display our new description.&#x20;

## Adding a Description Field to the Books Table

1. Open MySQL Workbench and connect to your database
2. Right click on your books table and choose Alter
3. Add description bottom of the list of columns and make it a nvarchar(1000) (Why this data type?)
4. Press Apply and then Apply to save the table.

## Editing your Add/Edit Form

Just like in the Manage Articles tool, we are going to use a \<textarea> as the basis of our WYSIWIG. The JS and CSS which we pasted are already in place in the index.bxm file. However, we do need to add the JS which transforms the textarea to a WYSIWYG entry. \
\
1\. Add the following code to your add/edit form:

```
<div class="form-floating mb-3">
    <textarea id="description" name="description" class="form-control" >
        #bookinfo.description#
    </textarea>
</div>
```

2. Add the script to convert the textarea. Make sure your license key is in the correct place and that the id of your textarea is in the correct place in the script.&#x20;
3. Make sure your server is started and open the Manage Books tool. Did it work?

## Adapting our queries to accommodate the new field

When we submit our form, there is a data chain that starts with submitting the form and ends up with the information being saved to the database. We need to add our description field to all of those.&#x20;

1. Does the text area have a name property?
2. When the form is submitted, is form.description passed to common.saveBooks()?
3. Does common.saveBooks() expect the parameter description to be passed to it?
4. Does description appear in the insert portion of the query?
5. Does description appear in the ON DUPLICATE KEY portion of our query
6. Does Description appear as a value in our parameter structure that gets passed into queryExecute along with our SQL?&#x20;

When this chain is complete, our data will persist to our database and be available to display on the front page.&#x20;

## Adapting the Details.bxm Page

We need to adapt the details page in the public facing area of the website to show the description. In the details page, add:

\<div>Description: #bookinfo.description\[1]#\</div>

to the book details area. Save and upload details.bxm.

Did it display correctly? Go back and edit the description and use the controls to add some more HTML including links, bold, italicized etc. Save it and look at the details page again. Did it work?
