# Case Types and Naming Conventions

One thing you might have already noticed in working with ids and classes in HTML is that things have names. Computers have names, websites have names, web pages have names, HTML elements can have multiple names with ids and classes. Databases have names, Data tables (we’ll get there) have names, Data fields (think columns in Excel) have names. Everything has a name. With that many names flying around, it is very easy to start getting confused as to what refers to what. As a result, conventions have come into play to help make code more readable. As we add more and more items into our conversations about databases and code, I’ll write out the naming conventions that go along with it. However, as always, first some concepts.

* Do not use spaces in your names. This includes filenames, IDs and Classes in web pages, databases, tables, fields or anything else. Even though technically you can put spaces in a URL, it’s only because the browser replaces the space with special codes to make it work. When we get into more complicated things, the spaces will flat out not work or will make the code much more complicated and less readable.
* If there are no spaces and we want use clear names, how do we handle names with compound words? Here are several ways to write them out:
  1. Pascal Case: Compound words are concatenated started with a capital letter. i.e.: “My Web Site” becomes MyWebSite. Often this is used for the names of classes and files.
  2. Camel Case: Compound words are concatenatedand started with a lowercase letter. i.e.: “My Web Site” becomes myWebSite. Often this is used for variable names (we’ll talk about variables later in the course).
  3. Snake Case: the words are separated by an underscore. All the words are lower case. “My Web Site” becomes “my\_web\_site”.
* But can’t we use a hyphen (-)?: Well, yes but down the road it’s going to become more difficult to distinguish what is a name of something and when you are telling the web page to do subtraction.