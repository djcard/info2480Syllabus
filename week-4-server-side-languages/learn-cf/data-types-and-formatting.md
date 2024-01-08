# Data Types and Formatting

Last week, we read an article called _Introduction to Data Types_ and used it to create the databases in the SQL server. Those datatype concepts are very much alive and well here as well. For example, what is the difference between 123456789 and 123,456,789? To a human, nothing. To a computer, almost everything. Let's look at it.

123456789 is a **number**. 123,456,789 is a **string**. Remember that numbers can ONLY have numerals, a decimal point and perhaps a positive or negative sign (depending on if it's an integer, a float, signed or unsigned).

There are some computer programs that are very strictly typed. That means that whenever you are talking about number, dates, or other data types, you need to specifically say that THIS IS AN NUMBER. THIS IS A DATE. ColdFusion, however, has both a reputation and culture of trying to do things in an elegantly simple way. It really does try to make things as straightforward as possible (one of the reasons I love it). Therefore, you don't need to announce to your application that you are now dealing with a number, the program gives it its best guess and, for the most part, it does pretty well. However, even if you don't SAY what type of data it is, the program still has to treat your information as if it is a particular datatype. Therefore, if you try to add two numbers #5+3#, you will get 8. If you try to add a string and a number you will get something else. See:

* \#5+3# = 8
* \#fish + 3# = variable \[FISH] doesn't exist

In this case, it's trying to treat the word "fish" as a variable and, since we haven't covered those yet, we'll gloss over that. SOOOOO, does that mean that we are forever, forced to look at numbers like 6234798723847932 with no commas, dollar signs or any other human readable features? Of course it doesn't. This brings up the concept of **formatters**. There is, or can be, a difference between the underlying type of data and how it is presented on the screen. CF (and other languages) does this with what are called "formatters". CF has several. We're going to look at two of them.

**Number Formatters** - Let's look at our example: 123456789. A nine digit, hard for humans to read, number. With a Number formatter we can specify that this number should have commas and, just for fun, a dollar sign. We can do that like this: #Numberformat(123456789,"$,")# and we get $123,456,789. We told the formatter to put in a $ and a , in the default places and it did. The second part of this is called a "Mask". The point here isn't that you need to learn the exact syntax for the NumberFormat Mask since it's in the CF Documentation here: [https://wikidocs.adobe.com/wiki/display/coldfusionen/NumberFormat](https://wikidocs.adobe.com/wiki/display/coldfusionen/NumberFormat) but that you know the concept.

**Date Formatters** - Dates are another of those things that are inherently human readable. What does a date look like to the computer? Like this: {ts '2022-02-06 20:18:11'} . That particular format is called a **TimeStamp**. You can read it and once you get past the {} and the quotes you can see the date and the time in 24hr format including the hours, minutes and seconds. So how do you get the date to appear on the screen? This is done by calling a ColdFusion **function**. A function is a list of instructions that you can give to a computer or programming language to perform. Most functions,at least in CF, have names and can be referenced simply by calling its name. In this case we are going to look at a common function to get the current date and time as a date and is called now(). It's very difficult so pay attention: To make it work you type #now()#. Whew! Complex, right! Of course it needs to be inside a \<cfoutput> tag but you already knew that ;) Whenever you see "()" it almost always means that there is a function being called. The parentheses are important for reasons we will look at later .

**Exercise**: There is a folder in your site called "LearnCF" which, in turn, has a folder called "exercises". If it doesn’t have a folder called “exercises”, create it. Make a new web page called "MyDate.cfm" in that "exercises" folder. In the body tag, add \<cfoutput>#now()#\</cfoutput>. Start up your local server and open this page. You should see the current date and time as a time stamp.

However, it's usually not a good idea to make your audience work very hard for seemingly simple things like the time. Therefore, let's look at the Date Formatter: The syntax is very similar to the Number Formatter in that is it looks like this: DateFormat(Date,"_mask_"). The trick is to then know what goes into making the mask. The documentation at [https://wikidocs.adobe.com/wiki/display/coldfusionen/DateFormat](https://wikidocs.adobe.com/wiki/display/coldfusionen/DateFormat) has a list of the elements of a mask. For example, to make the common date notation for the US, you would type #dateformat(now(),"mm/dd/yyyy")# and it appears like this: 2/06/2022

**Exercise**: Open up your MyDate.cfm page again. On the next 5 lines, use different masks (find them on the link above) to make the date appear differently.