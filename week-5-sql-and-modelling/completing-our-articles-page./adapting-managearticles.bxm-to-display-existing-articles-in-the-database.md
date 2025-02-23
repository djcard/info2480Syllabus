# Adapting manageArticles.bxm to display existing articles in the database

## Background

In [previous exercises](../../week-3-working-forms-and-our-first-table/working-forms/capturing-your-form-data.md), we created a form and corresponding server side code that allowed us to create articles with a title, description and status which persisted in our MySQL database. That was a good first start but to have an effective tool, we need to be able to see what articles are in our database and choose one to edit in addition to being able to create new ones.&#x20;

## Changing our page layout

The first thing we need to do is to change the layout of our page so we can see the list of articles on the left side and see our form on the right. We can do this using the `row` and `col` classes in Bootstrap. The instructions are below but for more complete information on this, please see [https://getbootstrap.com/docs/5.3/layout/grid/](https://getbootstrap.com/docs/5.3/layout/grid/).

1. To make rows and columns, we need to add a few \<div> tags to our page. Above the current form add this structure:

```html
<bx:output>
    <div class="row>
        <div class="col">
            This is for our list of articles
        </div>
        <div class="col">
            This is the new place for our form
        </div>
    </div>
</bx:output>
```

As you can see, we have a row with two columns in it. Because we have simply used the class `col` each of our columns will be of equal width. Bootstrap operates as if the page is 12 columns wide and each element can then be assigned a width from 1-12. If we want to divide our row in two columns which are 25% wide and 75% wide, we can use the classes `col-3` (3 is 25% of 12) and `col-9`  (9 is 75% of 12).  &#x20;

2.  Move your existing form into the area that says "This is the new place for our form". Your page should look something like this:

    <figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

## Creating our list of Articles

1. To get a list of the articles in our DB we need to create a function in our bookstore.common.articles.bx file. Let's call it "allArticles". Just like we did in the "saveArticle" function, we are going to use queryExecute() to send our SQL to the MySQL server to get our data. After doing the [Introduction to SQL](../introduction-to-sql.md) exercise, you should be able to write the SQL to retrieve the data we want. Can you? Your function in bookstore.common.articles should look something like this:\


```boxlang
    function allArticles( ){
        return queryExecute("SELECT * FROM articles");
    }
```

2. Back in our manageArticles.bxm page, we need to call that function and then use the results to make our list.&#x20;
   1. Move the line `<bx:set common = createObject("bookstore.common.articles") />` out of the \<bx:if> statement that it is in currently and up to the top of the page. We now need that common variable all the time, not just when we submit the form. This is the first thing that needs to run on the page so put it at the top.&#x20;
   2. The next thing we need to do is handle any form submission so keep the `<bx:if form.keyExists("title")>.......</bx:if>`  next. Remember that almost all template pages whether in pure HTML, BoxLang or other languages, are going to process from top to bottom so we need to keep things in the order we need them to happen.&#x20;
   3. Under the `<bx:if>` block, let's retrieve all of the articles from our DB. We are going to call the allArticles function on our common variable and store the results in a variable. Let's call that variable `allArticles` so it is clear what it contains.  Something like this:  `<bx:set allArticles = common.allArticles() />`
   4.  We now need to use the results in that variable to make our list. In the column we made above that says `This is for our list of articles`, we need to create an ordered list by using `<ol></ol>` tag. Inside that ordered list, we are going to LOOP over our query results and create one \<li>\</li> element for each item in our results. This whole section looks like this. Notice how we are looping over the query. We are using #id# and #title# to represent fields in our database. Each \<li>\</li> represents one row in our data table. \


       ```boxlang
       <ol>
           <bx:loop query="allArticles">
               <li><a href="#cgi.script_name#?id=#id#">#title#</a></li>
            </bx:loop>
         </ol>
       ```


   5.  When you open your page, you should see something like the image below. It won't be exact, obviously since it will show the titles in your database but the layout and functionality should be the same. Notice how, when you click on an item on the left, the same page opens but we are passing a variable called id in the URL query string which has the value of the article in the database.&#x20;

       <figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

