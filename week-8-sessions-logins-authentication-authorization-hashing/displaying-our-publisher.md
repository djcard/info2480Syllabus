# Displaying Our Publisher

In previous exercises, we added a select control to our Manage Books page (addEdit.bxm). However, we haven't completed the process of displaying the publisher on the search resutls page on the front of our website (details.bxm).&#x20;

The details.bxm template is populated by a query from bookstore.common.books in the searchBooks() function. Currently, that query is returning everything from out books table including the publisherId. We can add that to our display but all we are going to see is the actual Id of the publisher like this:

```boxlang
<bx:output> 
    <image src="/bookstore/common/images/#bookinfo.image[1]#" style="width:300px;float:left; margin:15px"/>
    <div>Title: #bookinfo.title[1]#</div> 
    <div>ISBN-13: #bookinfo.ISBN13[1]#</div> 
    <div>Year: #bookinfo.year[1]#</div> 
    <div>Weight: #bookinfo.weight[1]#</div>
    <div>Publisher: #bookinfo.publisherId[1]#</div>
    <div>Description: #bookinfo.description[1]#</div> 
</bx:output>
```

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>The rendered code in oneresults.bxm</p></figcaption></figure>

That doesn't help us very much since no-one know what publisher "1" is. What we want to do is display the information in the Publishers table which corresponds with the publisherId in the books table. We do this by adding a join to our query. The query which populates our details.bxm page is in the class `bookstore.common.books` in the `searchBooks` method. Currently, our query looks like this:&#x20;

```boxlang
select * from books 
    where title like '%#arguments.searchTerm#%' 
    or isbn13='#arguments.searchTerm#'
```

We add a join to our query like this:

```
select * from books 
    inner join publishers on books.publisherId = publisher.id
    where title like '%#arguments.searchTerm#%' 
    or isbn13='#arguments.searchTerm#'
```

Notice how we add the line `inner join publishers on books.publisherId = publisher.id` . This tells the SQL server to give us all the row in the books table and the row in the publishers table where the id in the publisher table is the same as the publisherId in the row in the books table. Make sense?

There are several different types of joins but we are going to focus on two: `Inner Join` and `Left Outer Join`&#x20;

* An inner join returns all the records in both table where there is a match and ONLY if there is a match. If nothing matches, no rows are returned.&#x20;
* The left outer join will return all the rows in the first table ( `books` in our case ) regardless if there is a match or not. If there is a match in the second table ( publishers ) it will return those fields as well.&#x20;

In your bookstores, adapt your queries and then edit your details.bxm page to display the name of the publisher ( not the id ).&#x20;

