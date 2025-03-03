# Adding Images to our

## Background

You aren't supposed to judge a book by its cover but even so, there are a huge amount of marketing dollars spent to make book covers look appealing. Let's add the ability to upload images to our system.

## Adding Images

This process is a little more elaborate.

1. We need to add 2 elements to our form.

`<input type=”file” name=”uploadimage”>`     \
`<input type=”hidden” name=”image” value=”#trim(bookinfo.image[1])#”>`\
`<label for="uploadImage">Upload Cover</label>`\
`<div class="input-group mb-3">`    \
&#x20;   `<input type="file" id="uploadImage" name="uploadimage" class="form-control" />`    \
&#x20; `</div>`

Why two? What are each of these tags going to accomplish?

We also need to make one more changes to our form tag.

1. add **enctype="multipart/form-data"** so it reads: `<form action="#cgi.SCRIPT_NAME#?book=#book#" method="post" enctype="multipart/form-data" >` This is because, while text boxes send information in plain text, images are stored as Binary objects and the form needs to be able to send both text and binary objects.
2. Because we have made this page a module which fits into a larger index.cfm, we also need to pass in what tool we are using. The action attribute, therefore, needs to change to reflect that.

\<form action="#cgi.SCRIPT\_NAME#?tool=#tool#\&book=#url.book#" method="post" enctype="multipart/form-data" >

`<form action="#cgi.script_name#?tool=addEdit&book=#book#" method="POST" enctype="multipart/form-data" >`

## Editing our DataTable

In the books table, add a column called image and make it an nvarchar(200).

## Handling The Uploaded Image

The image will be uploaded in the form but we need to handle the uploaded file with a few extra steps.&#x20;

1. Create a folder in the bookstore/common folder named images. This is where we are going to save all of our uploaded images.
2. Create a new method in bookstore.common.books named uploadFile which accepts a parameter called filefield.&#x20;

```
function uploadFile( fileField ){
   return fileUpload(expandPath("/bookstore/common/images/"),"uploadImage","*","makeUnique");
}
```

FileUpload takes 4 arguments. Arguments are data that are passed to a function in order for the function to run. In this case the four arguments are

1. Destination (The folder where the image will be sent) expandpath(**'/'**) & **/CodeBase/images/"**
2. fileField – The form field with the image data - **"uploadimage"**
3. accept – the types of images the upload will accept - **"\*"**
4. nameconflict – What should the upload do if there is already a file with that name in the destination folder. - **"makeunique"**

FileUpload returns a struct of data which looks like this:&#x20;

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

There are a number of items here but the one we are particularly interested in is the serverFileName property.&#x20;

5. Back in addEdit.bxm, inside our \<bx:if >...\</bx:if>statement, we are going to pass in the name of our fileField ( uploadImage) to common.uploadFile like this:\
   `<bx:set fileInfo = common.uploadFile("uploadImage") />`\
   and then\
   `<bx:set form.image = fileInfo.serverFileName />`

This will put the file name of the image into the form scope so we can save it along with the other information.&#x20;

6. Adapt the rest of the data chain to save form.image into your books table.



In our form, we added two \<input> tags – one with the type =”file” with name=“uploadimage” and the other type=”hidden” and name=”image”. Why two? Hopefully now you see that one (image) was to hold the value of the image that was already in the database. The other (uploadimage) was in case we wanted to upload a different file. If we do upload a new image, we process the upload, get the name of the new file and put it into the formData.image variable.

Can you also adapt your form to show the image if it is already in the database?

Can you adapt your front facing details.bxm file to display the image as well?
