# Functions

A function is a series of instructions that are given to a computer to be processed. A function can be written and then just sit there until it is called upon to do its job. We talked a little bit before about functions when we used now(). Now() is a function built in ColdFusion that gets the time from the operating system. You can also write your own functions as well. This allows you to break your code into smaller chunks which makes them easier to read and easier to manage. It also allows us to write certain functionality that we are going to use over and over again in a way that we only have to write it once.

Here is a simple example. We are working on a website where we need to frequently add two numbers together (I told you, it's a simple example). We could write a function that would add the two numbers together for us and put it on our site or our page so we can access it. Let's look at what this function could look like.

\<cffunction name="addNumbers" access="private" returntype="numeric"> <--- the tag to make a function is \<cffunction>. The **NAME** property is how we reference the function. **ACCESS** defines what type of code can access this function. In this case only this page can access it. **RETURNTYPE** says that this function can only return numbers.

\<cfargument name="firstnum" type="numeric"> <--- Information that a function needs to do its job are called "Arguments". Our function is going to add two numbers together so we need to pass in two numbers to it. That means that the function needs to have two variables already assigned to "catch" those variables. We will call the first number "firstnum".

\<cfargument name="secondnum" type="numeric"> <--- And the second number "secondnum"

\<cfreturn #firstnum+secondnum#> <--- This hands back the sum of the two numbers to whatever called it.

\</cffunction> <--- This closes the function.

Here it is as a whole:

```jsx
<cffunction name="addNumbers" access="private" returntype="numeric">
    <cfargument name="firstnum" type="numeric">
    <cfargument name="secondnum" type="numeric">
    <cfreturn #firstnum+secondnum#>
</cffunction>
```

Ok, great. So what, how do we use this? Now, to add 5 and 3, we don't need to type out #5+3#. We can type #addNumbers(5,3)#. This command passes in the number 5 as "firstNum" and the number 3 as "secondNum) and displays whatever comes back in its place.

This particular example doesn't necessarily save a great deal of typing but it does illustrate how a function works. You create the function, define the arguments that the function should expect. Write the code that the function should perform on the inputs and return the output.

You would call it like this:

\<cfoutput>#addNumbers(10,5)#\</cfoutput>

We also can assign variables to the value returned from a function. We can write \<cfset myNumber=addNumbers(5,8)> will assign the value of 12 to the variable myNumber

**Exercise**

In the exercises folder, create a page called MathFunction.cfm. On it, type out the function that's displayed above. Put it at the bottom of the page to keep it organized. Above it, call the function and pass in several different combination of numbers (i.e. #addNumbers(5,3)#\<br/>#addNumbers(100,223)# etc.

**Bonus Exercise**: Can you make a form that accepts two numbers, submits it to the same page and then uses the function to add the two numbers together? All the information you need is in these docs.
