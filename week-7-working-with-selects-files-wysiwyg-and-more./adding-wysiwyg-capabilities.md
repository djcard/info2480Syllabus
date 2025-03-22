# Adding WYSIWYG Capabilities

## Background

WYSIWYG (pronounced Wiz-E-Wig) stands for What You See Is What You Get. It is a tool that a non-programmer can use to edit text, format it like you can in a word processer and the HTML is written behind the scenes automatically.

One of the most popular WYSIWYG tools is called CKEDITOR, an open source library written in JavaScript,that allows a form element to be turned into a WYSIWYG editor. We are going to use CKEDITOR in two places

1. The Manage Articles page (manageArticles.bxm)
2. The Manage Books (addEdit.bxm)

There are three initial steps to adding this feature to our Manage Articles tool.&#x20;

1. Creating a free account at [https://ckeditor.com/](https://ckeditor.com/)
2. Adapting our manageArticles.bxm page.
3. Retrieving the free license key from [https://portal.ckeditor.com/](https://portal.ckeditor.com/)



## Creating a Free Account at [https://ckeditor.com/](https://ckeditor.com/)

In the recent past, CKEditor has changed from being an open source first to a paid product which happens to have a free version. It is still a good product and we can use the development license for class without having to pay a license fee.&#x20;

Visit https://ckeditor.com and click on either `Register for a license key` today or `Start a free trial`.  You will need to fill out some info and choose a password. YOU SHOULD NOT HAVE TO PUT IN ANY PAYMENT INFORMATION.&#x20;

## Adapting our manageArticles.bxm page

1. Open bookstore/manage/index.bxm
2. Visit [https://ckeditor.com/docs/ckeditor5/latest/getting-started/installation/cloud/quick-start.html](https://ckeditor.com/docs/ckeditor5/latest/getting-started/installation/cloud/quick-start.html).&#x20;
3.  Copy the link to the CSS file and paste it into the \<head>...\</head> tag.

    <figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>
4.  Copy the link to the JavaScript file and paste it into the head tag as well.&#x20;

    <figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>
5. Open bookstore/manage/manageArticles.bxm
6.  &#x20;Copy the JavaScript command to actually change a textarea tag to our WYSIWYG tool. Make sure that the code you copy from the website looks like it does below. If there is a  \<!\[CDATA\[..../> or similar tag surrounding the JS code, make sure you remove it.&#x20;

    <figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>
7. Visit [https://portal.ckeditor.com/](https://portal.ckeditor.com/) (you'll need to sign in first). Go to License Keys and copy the developer license. Paste it in the script above where it says \<YOUR\_LICENSE\_KEY>
8. Find the id of the textarea element on your manageArticles.bxm page and replace where it says 'editor' in the script above with the id from your textarea.&#x20;
9.  Make sure your server is running and open your bookstore/manage/ area. Choose an article to edit. Did it work?

    <figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>
10. After editing an article and adding some bold elements or chaging the font color using the controls in the toolbar which should appear, save is and look at that article on the front page of the public area. Does it look differently?

##
