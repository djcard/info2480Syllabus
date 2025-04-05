# Adapting Our Database

The first step is to adapt our database to both store a list of genres we wre going to need and then to store which book is assigned to each genre.&#x20;

1.  Create a table called genres with fields id ( an autoincrementing integer ) and name (nvarchar(20)). Populate this table with several genres such as Mystery, History etc. Search for a list of Genres if you need some ideas.&#x20;

    <figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
2. Create a tables called genresToBooks with genreId (id) and isbn13((varchar(17)). In this table, notice how both columns are listed as a primary key. That will help us ensure that we don't have duplicate listings for a particular book to a particular genre. We can add a book many times to different genres and a genre many times to different books but only once for each combination. This is called a compound primary key.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

## Types of Relationships

When we set up our books
