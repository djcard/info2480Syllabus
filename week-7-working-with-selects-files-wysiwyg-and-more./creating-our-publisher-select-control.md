# Creating Our Publisher Select Control

### Populating our Publisher Table

In MySQL Workbench, right click on the publishers table and choose  Select Rows - Limit 1000. This will allow you to manually enter data into the cells. Populate three or 4 rows of publishers and click on apply. This will commit the data to the table.&#x20;

### Adding the Publisher Input

The publisher input is going to be a type of input called a “select” tag. It’s also called a “drop down” and I’m sure a few other things. A \<select> has a name just like the other form inputs we’ve looked at.  Within the \<select> and \</select> are a series of \<option> tags which define, you guessed it, the options that available in the select tag. Here is a simple select tag:

```html
<select name=”publisher”>         
    <option value=””></option> 
</select>
```

This select has one option which is blank. This is a typical setup for a select since there is usually a blank option at the top, so it appears blank. This makes it clear that a value has not been chosen. We are going to use a query to get all the publishers in our database and make options from the data we get back. We are also going to make it so that the correct publisher is selected if one has been set.

1. In bookstore.common.books create a new function called allPublishers. Can you do this by using the other functions in the component as an example?&#x20;
2. Add a call to the allPublishers function from addEdit.bxm.

<**bx:set** allPublishers = common.allPublishers()>

Use the results of this query to make the other options in our select:

```
<div class="form-floating mb-3">
    <select class="form-select" id="publisher" name="publisherId" aria-label="Publisher Select Control">
        <option ></option>
        <bx:loop query="allPublishers">
            <option value="#id#">#name#</option>
        </bx:loop>
    </select>
    <label for="publisher">Publisher</label>
</div>
```

**Don’t forget to add the NAME attribute to the select control.**

A \<select> tag can have only one of its options selected at a time. The selected options value is the value passed when the form is submitted. We are using the id (which should now be populated with UUIDs) as the value being passed. We don’t want to see the UUID when we open the menu, we want to see the name of the publisher. Therefore, we are putting the NAME field between the \<option> and \</option> tags. This is what appears in the dropdown.

Save the file and upload it. Did it work?

We still need to make it so that the correct option is selected when one has been chosen. In order to make that happen we need to set the SELECTED attribute of the option where the ID in the PUBLISHER table is equal to the PUBLISHER field in the BOOKS table. Can you think of how we can make that happen? We need to find a way to drop the word “selected” as an attribute in the option tag If the ID is equal to the PUBLISHER field in books.

We’re going to use something called a “Ternary Condition”. This is a short hand way of doing an “if-else” statement which makes for very clean, concise and readable code. Add the bolded text below to the \<option> tags in the publisher drop down.

`<option value="#id#" #id == bookinfo.publisher ? "selected" : ""#** >#name#</option>`

Let’s unpack that

| Code                            | Description      |
| ------------------------------- | ---------------- |
| id eq thisBookDetails.publisher | This is the “IF” |

“id” is the value from the publishers table. thisBookDetails.publisher is the publisher field from the query about the book we are editing.

"==" is the BoxLangsyntax for “is equal to”. Note a few things

1. a single “=” assigns a value as in var x=5. Two equals “==” is comparing two values.
2. JS also uses “===” but BoxLang does not. Why is that?

Did it work?
