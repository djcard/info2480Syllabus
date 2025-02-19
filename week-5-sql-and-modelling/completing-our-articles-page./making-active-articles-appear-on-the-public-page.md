# Making Active Articles Appear On The Public Page

## Background

The whole point of the articles is to appear on the front page of our bookstore. To that end, we have a few more quick edits.&#x20;

## Editing our allArticles function to have a status argument

On the main page of our site, we want only articles which have status==1 to appear. However, we are already using allArticles in our manageArticle.bxm page and we want it to show all articles so that we can edit them. There are several ways we can reconcile these differences.&#x20;

We do NOT want to create a new query, however, because of a principle called "DRY" which stands for Don't Repeat Yourself. We don't want another function which is almost entirely the same as an existing one. This increases the amount of code we have to maintain and gets hard to read and debug.&#x20;

Instead, we're going to adapt our existing allArticles function.&#x20;

1. Add an argument called id and default it to -1 since our current use case wants to show all articles not just ones that are status==1 or status==0.&#x20;
2.  We need to insert a condition into our SQL. Something like "where status = 1", but we don't want that condition to be there if no status is submitted. If we add this line inside our function but above, the queryExecute(), we can create the string we need. If we don't submit a status, we have an empty string. If we submit a status, we get our condition.&#x20;

    ```boxlang
    var extra = status > -1 ? "where status=#status#" : "";
    ```
3.  We now need to put that extra variable into our query. Our entire function now looks like this:\


    ```boxlang
        function allArticles( numeric status=-1 ){
            var extra = status > -1 ? "where status=#status#" : "";
            return queryExecute("SELECT * FROM articles #extra#");
        }
    ```

## Adapting our horizontalNav.bxm page to display our article titles

Turning to the public side of things, we need to adapt our horizontalNav.bxm file to display the titles of articles we want users to choose from to read.&#x20;

1.  We need to first create an instance of bookstore.common.articles like we did on our manageArticles.bxm page.&#x20;

    ```boxlang
    <bx:set articles = createObject("bookstore.common.articles") />
    ```


2.  We then need to call the allArticles function passing in status = 1

    ```boxlang
    <bx:set allArticles = articles.allArticles( status=1) />
    ```
3.  Lastly we need to loop over the query to create an item in our nav bar on which to click. We will need to pass in the id so we know which article to display, but we will also need to pass in one more piece of information which we are going to call "t". In this case, t will always have a value of "articles".  We will go over what "t" is for in the next section.&#x20;

    ```boxlang
     <bx:output query="allarticles">
        <li class="nav-item">
            <a class="nav-link" href="#cgi.script_name#?id=#id#&t=articles">#title#</a>
        </li>
     </bx:output>
    ```
4. Open your public facing page ( /bookstore/public/index.bxm ). Do your active acticles appear in the top nav bar? If you go back to the management page, edit an article and make it active or inactive, does the corresponding article appear or disappear on the public page?

## Using "t"

You might have noticed that, while we can click on the title of an article, the actual article doesn't appear. This makes sense since we haven't told it where to show up. Ideally, we would like the carousel to go away and our article to show up in its place. We can do that by making the template which appears to be dynamic instead of static.&#x20;

1.  In the /bookstore/public/index.bxm file, find the line where it says&#x20;

    ```boxlang
    <bx:include template="carousel.bxm" />
    ```
2. Change "`carousel.bxm`" to be "`#t#.bxm`". This is now include the file which corresponds to whatever the value of "t" is. For example, if t="hello" then this will include "hello.bxm". If you open this page now, it is expected that you'll receive an error since we now are using a variable and haven't set a value for that variable yet.
3.  At the top of the page, we need to set a parameter for "t".&#x20;

    ```boxlang
        <bx:param name="t" default="carousel" />
    ```
4. Now need to create a file called "articles.bxm". Create that and simply put "Here are articles". Visit the /bookstore/public/index.bxm page and click on one of the articles in the navbar. Does your new page appear?

Creating Articles.bxm.

1. At this point you have all the tools you need to create /bookstore/public/articles.bxm using the other pages as example.&#x20;
   1. Create a variable creates an instance of bookstore.common.articles.
   2. Call the function which queries the articles table based on the id submitted.&#x20;
   3. Display the title and description fields on articles.bxm.
