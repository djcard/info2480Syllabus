# Intro To Variables

A variable is a place holder. That's it. Fairly straightforward in concept. It gets a little more complicated in practice but, really, that's it. We're used to seeing variables in math classes which are usually called X and Y and other mundane things. In programming, we can certainly do that, but more often we use words that are more descriptive. For example we might have a variable for the price of a book and call it priceOfBook (remember that document on cases? Here's where it comes in). We might have a billing application and have a variable called dayBillIsDue and, surprise, it's the day that the bill is due. The name of the variable helps to describe what the variable does.

In ColdFusion, the \<cfset> tag is used to set or alter variables. For example, \<cfset myDogsName="fido"> creates a variable named "myDogsName" and sets the value of it to "fido". Seems straightforward enough. That means that myDogsName is a variable that contains a string. Remember how I said that ColdFusion was a "typeless" language? That means that I can just as easily make my variable equal a number, a date or anything else without changing any of that syntax. \<cfset dayBillIsDue = now()> will set the variable dayBillIsDue to today. To display the variable we surround it by #s as in #dayBillIsDue# which will display the date and time it was when we set it.

Exercise: Create a new web page called myVariables.cfm in the exercises folder. In the body tag type the following:

```
	<cfset todayDate=now()>
	<cfoutput>
		#todayDate#
	</cfoutput>

```

What did you get? This: {ts '2022-02-06 21:05:47'} ? If not, check your spelling and make sure all the tags are there.

However, notice that it's in the Java TimeStamp format. How do you fix that? Psst, the answer is two pages ago.

**Exercise**: Make the next time in your MyDate.cfm page a more readable version of the todayDate variable BUT don't change the underlying variable.

Were you able to figure it out? It quite possibly might be a dateFormatter but that's just a theory.

Which brings up a good point: if a variable can be anything (date, number, string) and we need it to be something in particular, how can we check and see type of variable it is? CF (and other languages) give us a way of testing the TYPE of a variable as well as the value of that variable. For example, to test if something is a date you can type #isdate(variablename)#. We can see if our todayDate variable is a date by typing #isDate(todayDate)# and we get: true . ColdFusion outputs Booleans (Yes/No variables, remember?) as literally YES or NO. You can also use True or False, 1 or 0, or blank and non-blank to set a boolean but it will display as YES/NO.

**Exercise**: On the myVariables.cfm page put a \<hr/> tag under the first part of the page and in this second, add up the price of your 10 books in your Excel Project. Can you do it with only one variable name? Let's call it totalBookCost. Hint: Start with \<cfset totalBookCost=0> and go from there. Think you can do it? Don't forget to output the final amount to the page.
