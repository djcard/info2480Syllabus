# Completing ManageArticles.bxm to Edit Existing Articles.

## Background

Now that we have a list of the titles from our articles database on which we can click and send the id through the URL, we can adapt our form to both create and update articles.&#x20;

## Putting in some Flow Controls

The flow is how the page works as you use it. What happens first? What happens second? and so on. The basic flow of our page is going to be

1. Open the page and see a list of articles. We can then choose to edit an article or create a new one. We do not see the form yet.&#x20;
2. One we choose to either edit an article or create a new one, the form appears which allows to enter data.&#x20;
3. When we create or edit a new article, the changes should save when we submit the form and all of the changes should be reflected on the page immediately. For example, if we add a new article, that new article should appear in the list on the left. If we edit an articles' title, the new title should appear on the left, not the old on.&#x20;



## Making our Form only appear when we choose to edit or create an article

To make this happen, we need to put in a \<bx:if>\</bx:if> statement. the thing we have the most control over at first is the ?id=## variable in the URL. Let's use the following logic

* If the id is 0 - show the form to create a new article
* If the id is 1 or higher - show the form tto edit an existing article.&#x20;
* If the id is -1 - do not show the form at all.  This should happen when the user first arrives at the page and has not chosen an article to edit or to create a new article.&#x20;

1. To make the id default to -1 and therefore hide the form, we need to add a \<bx:param> component. On the very first line of the page, add \<bx:param name="id" default="-1" />. This is the new "first thing" we need to happen. This will create a variable called id if one has not been submitted through the URL or the form. If it has been submitted, this new id variable will use that value.&#x20;
2. Wrap the form with \<bx:if id gt -1>.....\</bx:if>. This will make the form only appear if the id is 0 or higher. Open a new browser tab and navigate to manageArticles.bxm. Did your form appear? It shouldn't have.&#x20;

## Adding a Create Article link

1. In the list of articles on the left hand side, we looped over a query to create \<li>\</li> elements inside a \<ol>\</ol> tag. This shows the existing articles but not a link to create a new one.&#x20;
2. After the \<ol> but before the \<bx:loop> tags, add a structure that looks like this: \<li>\<a href="#cgi.script\_name#?id=0">Create New Article\</a>\</li>. This will tell our page to show the form since we are going to create a new article.&#x20;
3. Reload the page and click on Create New Article. Did the form appear?
4. Enter the data for the title, body and check active. Submit the form. Did it save? Did your new article appear on the left hand side?



## Editing Articles

We already have the ability to choose a title and pass in the ID. We now need to tall our form to query the database for the article.&#x20;

1. In bookstore.common.articles, create a function called articlesById which accepts one argument which is id.
2.  Use queryExecute to send the SQL to retrieve that article from the database and then return the results. Something like this below. <br>

    ```boxlang
        function articleById( required numeric id){
            return queryExecute("SELECT * FROM articles where id=:id",{id:arguments.id});
        }
    ```

&#x20;3\. We need to call that function and when we show our form. Let's make a variable called accountDetails and use that to store the results from our query. Inside the \<bx:if id gt -1> tag, put in&#x20;

```boxlang
<bx:set articleDetails = common.articleById(id) />
```

4. We then need to show the results of our query in each of the \<input > tags in our form. For each input add the value property.&#x20;
   1. For the title input, we would add value="#accountDetails.title#".&#x20;
   2. For the body input, we would add value="#accountDetails.description#".&#x20;
   3. For the active checkbox we would add something a bit different. we need to put the checked property in the \<input> tag if the status is equal to 1. We do this like this: #articleDetails.status==1 ? "checked" : ""#.
   4. Lastly, we need to add another input to the top of the the form for the id since we now need to pass that in so the system knows what id to update. \<input name="id" value="#accountDetails.id#" />
   5. Reload your bookstore management page. If you click on the a link on the left, does your data show up in the form? If you submit it, it won't update in the DB just yet but it should appear and submit if you dump out the&#x20;

## Saving Our Edited Articles

Because we are now submitting our article with an ID, we need to make some changes to the query persisting our data to the database.&#x20;

Currently it looks like this: `INSERT IGNORE into articles (title, description, status) VALUES (:title, :description, :status)` . This works fine if we are only creating new articles but will not update existing articles.&#x20;

Our new query looks like this:&#x20;

```boxlang
INSERT into articles (id, title, description, status) 
     VALUES (:id,:title, :description, :status) 
     ON DUPLICATE KEY UPDATE title=:title,
     description=:description,status=:status
```

This will try to insert the data submitted BUT if the id already exists in the database, it will update the data instead. This is because we set the ID field to be what is called the primary key. The primary key is what make one row unique from every other row. Even if two rows have the exact same values for every other field, the primary key HAS to be unique to distinguish one row from another. If a primary key is established, the database will not allow a row with the same value for the primary key to be inserted.&#x20;

Try editing choosing and editing an article now. Did it work?
