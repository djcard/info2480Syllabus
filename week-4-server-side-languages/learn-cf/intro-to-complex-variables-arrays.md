# Intro To Complex Variables: Arrays

Objects are everywhere. In fact, in JavaScript and a few other programming languages, everything is ultimately an object but that's getting kind of abstract at the moment. Another type of complex variable we are going to work with are called Arrays. Whereas with objects/structs you can refer to the keys by name, the data in an array is sorted by number. This is very handy when you don't know the names of the keys you are working with, need to keep things in order, or have multiple objects with the same set of keys (like multiple books) and you need to keep them separate.

If it helps, you can think of arrays like a bookshelf that can keep getting longer and longer dynamically as you add things to it. When we add another index, we just add another shelf. Easy enough. We can then refer to the shelves by number as in myBooks\[1]="Hello". This means that in the Array "myBooks", the item located at index 1 is a string with the value of "Hello". Which highlights a difference between CF and most other languages. When most computer languages start to count (as in the first shelf of an array) they start with zero. They are called zero based langauges. CF starts with 1. Why? No idea but it does. At the time it made sense, I suppose and we'll go with that. That little fact comes up occasionally and I wanted to throw it out there now.

Here is how we would create a new Array in CF:

```
<cfset myArray=ArrayNew(1)>
<cfset myArray[1]="Hello">
<cfset myArray[2]="Goodbye">
<cfset myArray[3]=StructNew()
```

We can also add items to the Array by using ArrayAppend(myArray,"whatever") which will add the string "whatever" to the end of the array called "myArray". That's handy if we don't know what number we're on and just want to add something. We can dump that out the same way by using \<cfdump var="#myArray#" label="MyArray"> and we get this:

See how the items are lined up and numbered. These will stay in this order unless you change them. In an object, the keys can be displayed in any order by the application unless you take specific steps to code in a way that they display in a particular order. Arrays will always stay ordered.

The number in the parentheses is important. What it refers to is the how many dimensions the array has. Getting into multi-dimensional arrays is beyond what we are going to work with here so for now, just put a 1 in the ()

Does CF have a similar shorthand for arrays as it does for the objects? Yes. Arrays are denoted by \[]. To make the same structure as above would look like this:\<cfset myArray=\["Hello","Goodbye",{}]>

**Exercise**: Create a file named "myArray.cfm" in the exercises folder. Create complex objects using the same model you created on the last page and populate three more of them with three more books from the 10 Books Exercise. Put one of the objects in its own index in an Array and dump it out. Are you starting to see how an array of objects can be a powerful thing? If not, no stress but stay tuned. I know that this exercise is repetitive. In a few screens we are going to see how we can make the computer create the objects and arrays we want more easily and automatically. For now though, just type it out.
