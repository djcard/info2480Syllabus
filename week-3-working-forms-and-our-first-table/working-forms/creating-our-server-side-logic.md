---
description: >-
  Goal: By the end of this document, you will have created a .bx file to handle
  saving data from our first form and into your database.
---

# Creating Our Server Side Logic

Now that we have a working form, we can use the form data and save it to our database. To do that we need to do four things

1. Tell our manageArticles.bxm file to only send data when it receives it from the submitted form.
2. Create a CLASS file which saves data to our DB
3. Tell our manageArticles.bxm file where to send it the data it receives
4. Check the database to see if it saved.

## Telling our manageArticles.bxm file to only send data when it receives it from the form.&#x20;

You might have noticed that the green dump appears on your manageArticles.bxm page even where there is no data submitted. This is because all data submitted in a form is collected and saved in a special variable called "FORM". That variable exists whether a form has been submitted or not.&#x20;

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

To tell if our form as been submitted or not, we can add an IF statment and put some instructions inside of that. These instruction will run only IF the conditions in the statement are fulfilled.&#x20;

1.  Edit the top of your manageArticles.bxm page to this

    <pre><code>&#x3C;bx:if form.keyExists("title")>
    <strong>    &#x3C;bx:dump var="#form#" />
    </strong>&#x3C;/bx:if>
    </code></pre>
2. Load your page.  You should NOT see the green dump out box.&#x20;
3. Enter some data into your form and submit it. Now you should see the contents of your form displayed in the green dump out box like before.

## Create a CLASS file which saves data to our DB

Since we want to follow good separation of concerns, we are going to put all of our "controller" or "logic" in its own folder structure. Inside the bookstore folder, create a folder named "common".

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

1. In the common folder, create a file called articles.bx. All of the logic which has to do with articles, we are going to put into this folder.&#x20;
2. At the top of the file, put in: \
   `class {`\
   \
   `}`
3.  Now we are going to create a function inside that class. A function is just a collection of code that has a name and can be called whenever it is needed. We'll go more into functions next week but for now, just follow the code here. We're going to name our function `saveArticle`. \


    ```boxlang
    function saveArticle( ){
       
    }
    ```
4.  Our function is going to need several pieces of data to do it's job. In the parentheses after the function name, we are going to list the pieces of data it is expecting, what type of data it should be and whether or not it is required. \


    ```boxlang
    function saveArticle( required string title="", required string description="", numeric status=0 ){

    }
    ```

    \

5.  And now we need to actually put in the part of the code which will do the job we want. In this case, save our data to the database. \


    ```boxlang
        function saveArticle( required string title="", required string description="", numeric status=0 ){
            queryExecute("
                INSERT IGNORE into articles (title, description, status) 
                VALUES (:title, :description, :status)
            ",{
                title:arguments.title,
                description:arguments.description,
                status: arguments.status
            });
        }
    ```

## Tell our manageArticles.bxm file where to send it the data it receives

The last step is to tell our form to send our submitted data to our articles.bx file.&#x20;

1. In manageArticles.bxm, edit the if statement at the top of the page to this: \


<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

We are going to go over in much more detail what all of this code means next week but for now, let's see if we can get this working.&#x20;

2. Save the file.
3. Open your manageArticles.bxm page and submit the form.&#x20;
4. Don't worry if you have errors. They are normal and part of the process. Compare your code with the code here and see where it is different.&#x20;

## Check the Database

1. Open MySQL Workbench using the same direction from [before](../database-tools-and-your-first-db/connecting-to-your-mysql-database.md).&#x20;
2. From the left hand side under Schemas and your Username, expand Tables. You should see articles. If not, follow the directions [here](../database-tools-and-your-first-db/creating-your-first-table.md).&#x20;
3. Right click on arrticles and choose `select rows limit 1000`. An output of the data in your articles table should appear in the main part of the screen. Did it?
4. Let me know if you have any questions.&#x20;
