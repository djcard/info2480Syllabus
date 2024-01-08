# Adding WYSIWYG Capabilities

## Background

WYSIWYG (pronounced Wiz-E-Wig) stands for What You See Is What You Get. It is a tool that a non-programmer can use to edit text, format it like you can in a word processer and the HTML is written behind the scenes automatically.

One of the most popular WYSIWYG tools is called CKEDITOR, an open source library written in JavaScript,that allows a form element to be turned into a WYSIWYG editor. We are going to use CKEDITOR to add a “Description” field to our books table.

There are five steps to adding this feature.

1. Downloading and Linking to the JS library
2. Adding a description field to our books table
3. Editing the add/edit form
4. Adapting the update query to accommodate the new description field.
5. Adapting our details.cfm page to show the description

## Downloading and Linking to the CKEDITOR library

Note: The library might already be in your folders. This is a complete instructions as if it has not been downloaded. There is both a CDN and a downloadable package. You can use either but try to download the library and get it set up for the experience.

1. Go to [https://ckeditor.com/ckeditor-4/download/](https://ckeditor.com/ckeditor-4/download/)
2. Download the “Standard Package”. This will be a .zip file.
3. Extract the contents of the .zip file into your “includes” folder. If there is already a ckeditor folder, you can delete it. This will create a folder called ckeditor and several sub folders. Upload them all to your website.
4. In your /management/index.cfm page add the following line in the \<head> area: \<script src="/_loginname_/includes/ckeditor/ckeditor.js" type="text/javascript">\</script>
5. Upload the index.cfm page

## Adding a Description Field to the Books Table

1. Add a field to the books table called “description” and make it a nvarchar(max) (Why this data type?)
2. Save the table

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
