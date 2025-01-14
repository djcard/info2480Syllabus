# Creating An HTML Form with Bootstrap

Forms are everywhere on the web and we will need some for our project as well. Rather than walk you through this step by step, we're going to practice taking some HTML snippets from the Bootstrap docs and creating our page so that our design matches the Bootstrap examples.&#x20;

Our form is going to be in the `/manage/manageArticles.bxm` page and needs the following elements. Style them after the floating labels examples at [https://getbootstrap.com/docs/5.3/forms/floating-labels/](https://getbootstrap.com/docs/5.3/forms/floating-labels/)

* A text input with the label `Title`
* A textarea with the label `Body`
* A checkbox with the label `Active`

Here is a rough outline to get your started. Because /manage/manageArticles.bxm is included in /manage/index.bxm, the links to the Bootstrap library are already there. Only put the form on that page and no \<html>, \<head>, \<body> tags.&#x20;

\<form>\
&#x20;  \<input type="text">\
&#x20;   \<textarea>\
\
&#x20;   \</textarea>\
&#x20;   \<input type="checkbox" />\
&#x20;   \<button type="submit">Save\</button>\
\</form>

