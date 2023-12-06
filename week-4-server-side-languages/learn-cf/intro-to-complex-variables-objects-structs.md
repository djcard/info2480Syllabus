# Intro To Complex Variables: Objects/Structs

Up until now, variables have been fairly simple. Even in the data types document we were calling them simple variables. If we have simple variables, are there such things are complex variables? Well, yes, or there would be no need for the distinction.

If a string is simple variable and we can use a string to represent a book title, is there a way to put a group a number of variables together that are all related and have them work as a unit? For example, you've probably put together by now that each simple variable is like one of the cells in your Excel spreadsheet. Is there a way that we can refer to an entire row, in this case, an entire book?

Yes, and the answer is in using complex variables. There are many types of complex variables but they all boil down to two principle types: Objects and Arrays. That's it. Objects and Arrays. What are they? Good question.

Objects (also called **structures** in CF) are variables that you can attach values to by name. For example, I have an object named myCrayon that I am going to use to model a crayon. What are the properties that I am going to assign to it? Color? Length? Sharpened? Brand? Owner's name? We can do all of those. The overall point is that we can refer to the properties of the object by their names. We write this in two ways - The first is called "dot notation". It looks like this:

```
myCrayon.color="Blue Steel"
myCrayon.length=2
myCrayon.sharpened=true
myCrayon.owner="Timmy"
myCrayon.dateBought={ts '2022-01-10 23:18:49'}
```

Notice how these variables can be any of the simple data types we've already discussed? The first is a string. The second is a number (notice the lack of quotes around it). The third is a boolean. The fourth is a string and the fifth is a date. Can we attach complex objects to other complex object? Absolutely.

myMovie.name="Revenge of the Mutant Tomatoes"

myMovie.cast.Tim="Brad Pitt"

myMovie.sets.lowell.address="1 University Avenue"

In this movie example, myMovie is an object. The "cast" and "sets" variables are objects as is "lowell". What is nice about objects is that, because they have this dot notation, if we name our variables well, they can tell a story. It's easy to see that the address of the movie set in Lowell used in Revenge of the Mutant Tomatoes was "1 University Avenue", right?

Here is how you would create that in ColdFusion. CF calls Objects "Structs" and you do need to define them ahead of time, so to process to create the above example would look like this:

```
<cfset myMovie=StructNew()>
<cfset myMovie.cast=StructNew()>
<cfset mymovie.cast.Tim="Brat Pitt">
<cfset myMovie.sets=StructNew()>
<cfset myMovie.sets.lowell=StructNew()>
<cfset myMovie.sets.lowell.address="1 University Avenue">

```

This seems to be a good time to introduce to one of the most handy tags in ColdFusion and that is \<cfdump>. Many times when you are working with complex variables (or even simple ones) you need to see their value or what kind of structure they are. Yes, you can use all of the IsDate() or IsNumeric() or IsStruct() functions but it takes time to code and test each one and sometimes you simply want to just look at it for reference. \<cfdump> allows you to do just that. By typing \<cfdump var="#myMovie#" label="myMovie"> we get this:

See how the hierarchy is laid out with both the name of the properties and their values? Objects/Structs are also called **key pairs** which are made up of a **Key** and a **Value**. You would rarely want this to appear on your final working web page since it's not really glamorous even if it is incredibly helpful in your development. Just remember to take it off before you show it to your client or your boss.

You can refer to an object's contents a second way which is like this: myMovie\['cast']. This is called an **associative array**. You can also compound it and use myMovie\['sets']\['lowell']\['address'] and get 1 University Avenue or mix and match myMovie\['sets'].lowell\['address'] and get 1 University Avenue

**Exercise**: In the exercises folder, create a page called, "MyObjects.cfm" On it, take one of your 10 Books in Excel books and create a CF structure out of it. Use multiple structures to model an entire book including data from all four Excel Sheets (or SQL Tables). When you are done, dump out each of the objects you created.

***

Some people who have used other programming languages look at the tags above and ask, "Isn't that alot of typing? Isn't there a shorthand method to making objects????". The answer is "yes". That is alot of typing. Because of that, ColdFusion has implemented a shorthand to create structures. To use that shorthand, would look like this:

\<cfset myMovie={

```
cast:{

    Tim: "Brad Pitt",      

    Grace:"Stacy Dash"

},

Sets:{

    Lowell:{

        Address1:"1 University Ave"

    }

}
```

}>

Let's walk through that. The \<cfset mymovie= says we're going to create a variable called myMovie.

The { character says we are going to start a new object/structure.

The keys and values are separated by a : (colon) as in Tim:"Brad Pitt".

Different keys/value pairs are separated by a comma (,) as in between the two actors and the cast and set objects.

The } signifies the end of the object/struct.

Two ways to do the same thing.
