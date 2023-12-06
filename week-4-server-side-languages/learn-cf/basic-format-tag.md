# Basic Format: Tag

We’re going to start with the ColdFusion tag based format which looks very similar to HTML. For example, the \<cfoutput> tag is used to tell the CF server that we want it to process any CF code it finds between the \<cfoutput> tag and the \</cfoutput> tag. Just like in HTML, CF tags mostly need to be closed.

CF tags also can have properties and values. For example, \<cfloop from="1" to="10" index="i">....\</cfloop> means to start at 1 and do whatever is in between the tags 10 times using the variable "i" as a counter. We'll look more at the \<cfloop> tag soon but for now, see how the tag (cfloop) has properties (for, to, index) and values (1,10,i)? For the most part, like any other programming language, the thought process is:

1. What am I trying to accomplish?
2. What is the tag I need to do that?
3. What are the properties and values that that tag needs in order to do what I want?

Here are some other key issues:

1. All ColdFusion pages end in ".cfm", ".cfml", or ".cfc". We'll look at CFCs later so for now, make sure that all of your CF pages end in .cfm.
2. The Tag format is used almost exclusively when you need to put your CFML on the same page or amidst your HTML.
3.  ColdFusion makes extensive use of the # symbol. It uses it as a signal to the CF Server that it needs to process something. For example, a simple math problem is wrapped in #s like this: #5+3#. When the CF server sees that, it evaluates (or processes) what is in between and displays "8". A simple page that does this math problem would look like this:

    ```
    	<!doctype html> <--- Every HTML page needs a doc type

    	  <html>   <--- The start of every HTML page

    	  <head>   <--- The top part of every HTML page

    	  <meta charset="utf-8" /> <--- The encoding type that the text of the page is in (remember that discussion in the Introduction to Data Types document about Unicode and ASCII? This means this page is encoded in Unicode-8)

    	  	<title>Untitled Document</title> <--- The Title of the page, just like every other HTML should have

    	  	</head>   <--- The end of the head tag

    		<body>   <--- The start of the body tag, again like every HTML page

          	   <cfoutput> <--- Tells the CF server to pay attention to this area of the page (this speeds up the process by having the CF server only pay attention the portions for which it is needed).

          	     #5+3# <--- The actual CF code that does the math.

          	   </cfoutput> <--- The end of the cfoutput tag

    	  	</body> <--- The end of the body tag

    	  	</html> <--- The end of the html document

    ```
4. If the math problem #5+3# is NOT inside of a \<cfoutput> tag, it is just returned to the user as straight HTML so, since #5+3# in HTML is, well....#5+3# (not 8) it doesn't do much good.
