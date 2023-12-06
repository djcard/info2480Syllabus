# Forms And URLs

Each page has many variables present, even if you don't see them or declare them. These variables are grouped and placed in virtual buckets on the server and in memory. These "buckets" are called "scopes". There are several scopes we are going to use in this class but now we are going to look at two of them: the URL scope and the FORM scope.

**The URL Scope**

Look at the URL of this page. It is [http://127.0.0.1:51852/sources/learncf/index.cfm?p=urlforms](http://127.0.0.1:51852/sources/learncf/index.cfm?p=urlforms) . Have you ever looked at a URL and dissected it? The URL break down into several parts:

1. http:// - The protocol that is being used. Most websites use http:// or https://
2. 127.0.0.1:51852 - This is the domain name (and is listed in the DNS records to point to this computer)
3. /sources/learncf/index.cfm - This is the folder and file name of the page you are opening
4. ?p=urlforms - This part might be new. We are actually passing in named variables to the page which the page can then use for processing. In this case, whenever you click on a link on the left hand side, this same page is loading. However, based on the value of the "p" variable, different content loads. The "?" sign separates the page name from the variables or "query string" as it's called.

**Exercise**: Go To [Amazon.com](http://amazon.com/) and click on any of the items. Look at the URL. Somewhere in there is a ? which separates the name of the page and the variables that the page uses to render accurately.

Each language stores and processes these variables differently. CF stores them as a structure in a "bucket" called "URL". For example, if I use \<cfdump and type \<cfdump var="#url#" label="URL" />

you'll see a structure of all of the URL or "GET" variables that are being passed to this page. Copy this starting and including the "&" sign: \&name=Bob\&lastname=Marley. Paste it into the address bar AFTER ?p=urlforms so that it reads ?p=urlforms\&name=Bob\&lastname=Marley and press Enter to load the page. See how the dump of the URL variables changed above? The & sign is used to seperate one variable from another. the format is KEY=Value with no quotes.

**Exercise #2**:

1. **Copy** the index.cfm page from the /learncf folder into /learncf/exercises folder.
2. Create a blank page called toc.cfm (starting with no HTML tags etc). The entire page will consist of links, each one pointing to one of your exercise pages in the exercise folder. However, don't hardcode (type in) the name of the file. Use "p" as the name of your variable and pass in the name of the file to which you are linking. The href attribute should be something like 'href="index.cfm?p=myForm"'
3. If you want a sample, look at the index.cfm and the toc.cfm files in the learncf folder.
4. Can you figure out how your content is appearing? Are there any tags you need to remove from your exercise pages to make them work correctly?

**The FORM Scope**

The same can be used with form data. You might have created forms previous to this in HTML but without some sort of server side language, there is a very limited number of things you can do with that data. Now when we submit a form we can use the variables submitted in our page. Fill out and submit this form:

Name PleaseFirst NameLast NameEmail

See the output above? The form data is in a Struct called Form. We can access the individual pieces typing form._variablename_.

A form has several different tags in it. Here are the basics:

1. \<form action="#cgi.SCRIPT\_NAME#?#cgi.QUERY\_STRING#" method="post"> - The \<form> tag has two essential properties. The first is the "action" property. This is the file to which the browser will pass the form variables. Put another way, it's the page that will load when you submit the form. In this case, we are using CF variables that will automatically put the name of the same page. If you use this, don't forget to wrap it in \<cfoutput>The "method" property says how the variables will be submitted. The two most common methods are \<POST> and \<GET>. For the moment, let's keep it simple. Using "get" will put the variables and their values in the address bar or in the URL scope. Using "post" will submit them another way which is behind the scenes, not in the URL.
2. \<input type="text" name="firstname" placeholder="First Name" value="" /> - The input tag defines a place to put in a variable. You name the variable by using the "name" property in the \<input> tag. The value is whatever is entered by the user or you predefine with the value property.
3. \<input type="submit" value="save" /> - The \<input type="submit"> creates a button that will submit the form. You can also use a \<button> tag if you choose and by default this will submit the form.
4. For more HTML information about forms visit: [http://www.w3schools.com/html/html\_forms.asp](http://www.w3schools.com/html/html\_forms.asp)

**Exercise #3**: Create a page called myForm.cfm in the exercises folder (and don't forget to add it to your toc.cfm page). Use HTML to create a form which submits to the same page. Make your form with 5 inputs that coincide with the properties in your database. On the page put a \<cfdump var="#form#" label="The Form Data" /> tag so you can test the submission of the form.
