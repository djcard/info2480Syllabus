# Capturing Your Form Data

Previously, in [Creating An HTML Form with Bootstrap](../../week-2-review-of-html-and-css/creating-an-html-form-with-bootstrap.md), we made a form that submitted two value but had no way of seeing where the data went or had any way to access that data to do anything with it. A server side language allows you to capture, manipulate and use that data easily.&#x20;

## Prepping our Form

Previously, we were focused on making sure our form was visually appearing the way we wanted. Now we need to ensure that our form has all the properties present that we need to make the data usable.&#x20;

1. Open the manageArticles.bxm page in VSCode.&#x20;
2. Wrap your entire form in \<bx:output>     \</bx:output>. That will make sure that BoxLang will fill in any BoxLang variables needed.&#x20;
3. In your form tag, make sure you have these attributes
   1. action="#cgi.script\_name#" - This is one of the BoxLang variables. This will tell the page to submit the form data to this same page.&#x20;
   2. method="POST"  - This will tell form how the data is to be submitted.&#x20;
   3.  Your final form tag should look like this:&#x20;

       ```boxlang
       <form action="#cgi.script_name#" method="POST">
       ```
4. In addition to the type and other properties your input tags have, each of them should have a `name` property. \<input type="text" name="title" ...... />
5.  At the very top of your page put the line of code&#x20;

    ```boxlang
    <bx:dump var="#form#" />
    ```
