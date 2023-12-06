# Scripts And Components

In Week 2, we took a HTML page and split it up into several smaller .cfm pages in order to make the individual pieces smaller and easier to manage. However, all of these smaller files were still part of we call the “View\*”. The view is the part that the user sees and interacts. There is more code, however, that drives a website than just the view and we want to separate that into it’s own files. This is called Separation of Concerns ([https://en.wikipedia.org/wiki/Separation\_of\_concerns](https://en.wikipedia.org/wiki/Separation\_of\_concerns)).

In CFML, the view layer is typically found in “.CFM” files. Everything else can be found in “.CFC” files. CFC stands for ColdFusion Component. Technically, both .cfms and .cfcs can contain tag syntax and script syntax but for this class, everything that appears in a .cfm will be in tag and everything that is in a cfc will be in script.

What does a CFC look like? At its simplest, a CFC looks like this:

```jsx

component {
// Place your content here
}
```

There are no <> in sight. The component keyword is the first thing in the file followed by {. The very end of the file is } which indicates the end of the component.

Inside the component {}, there are functions which would look like this.

```jsx
component{
    function myFunction(){
    }

    function anotherFunction(){
    }
}
```

There can technically be any number of functions in your component but convention and “best practices” typically say to have around 10. That’s a guideline, not a “law”.

The first thing we need to do is “connect” the cfm and the cfc. This way, the cfm can access functions in the cfc and display the results. To do that, we assign the component to a variable in the cfm. This example assumes that the component is in the same folder as the cfm which is not always (actually, not usually) the case but it is a good place to start.

```jsx
<html>
    <head>
    </head>
    <body>
        <cfset myComponent = createObject("myComponent") />

				The product of my two numbers is <cfoutput>#mycomponent.multiplyTwoNumbers(5,7)#</cfoutput>
    </body>
</html>

```

Back in our component, we would then create a function called “multiplyTwoNumbers” that accepted 2 arguments and returned the product. It might look like this:

```jsx
component{
    function multiplyTwoNumbers(required numeric firstNum, required numeric secondNum){
			return firstNum * secondNum
    }
}
```

In the above component, the function multipleTwoNumbers accepts two arguments.

firstNum is required meaning that the function HAS to receive it or it will throw an error. It also has to be a number, or be able to be converted to a number, or it will throw an error. This means that the string “5” will still be accepted but the string “fish” will throw an error.

secondNum is the same as first num - required and numeric.

return firstNum \* secondNum ←— this means to multiply the two numbers together and return the product to the place that called it. In this case, this is the cfm page from where it was called.

**Exercise**: Create a file called “component.cfm” which is a CFM page and myComponent.cfc which is a component. In component.cfm, make a form that accepts 3 numbers. When the form is submitted, send the three numbers to a function in myComponent and display the product of the three numbers on the page.

\*not the TV show
