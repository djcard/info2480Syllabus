# Creating Content Pages

## Background

No matter how you look at it, content that appears on a web page needs to be written in HTML whether it is the output of sophisticated code or a simple paragraph about a bookshop. The question is, who is going to write all of that content? The developer? The marketing person? A third party? This is an important question since it dictates what tools are needed to make that appear.

These pages can be developed by someone who has been trained in HTML (and can therefore cost some bucks) and someone who hasn’t (who might include the owner, a temp or a marketing person).

If the developer is creating the content, perhaps they want to write it directly in a program such as Dreamweaver and then upload it. The temp or marketing person probably will not want to do that. Either way, it is safer and easier to have a tool where anyone with access can open a page, select an article of content, edit the content in a WYSIWYG and save it. This prevents coding errors, allows the site to look more uniform etc.

Outlined below are two methods to make the articles appear that correspond to the links across the top of our public page.

Steps:

**Method 1 (not preferred)**

1. Make a content page for each link you want across the top
2. Make the link across the top either point to that page or open the page you want as a module in the center area.

**Method 2 (Preferred):** Create a table called “content” with the fields, contentId, title and description.

1. Create a management page which lists all of the contents for “content” on the left side.
2. When you click on a title, present an edit form which allows the user to edit the title as an input text and the description as a WYSIWYG. Don’t forget to pass in the contentId to make sure you are editing the correct article.
3. Add a link to that “manage content” module to the management navigation bar.
4. If you are creating a new content item, use a UUID as the contented
5. In the public area, create a module that searches content based on the uuid submitted in the URL and then displays the title and the description of that article.
6. Change the links in the navigation area to open that page and pass in the correct UUID.

Make sense? The sample at [http://comweb.uml.edu/codebase/week9](http://comweb.uml.edu/codebase/week9) has a working system.
