# Adapting Our Management Page To Be Multi-Tool

Last week, we adapted our public facing index.bxm page to dynamically include whatever file we passed to it. This way we could display the carousel page when needed and the articles page when needed. We need to do the same thing to our management bookstore/management/index.bxm page.&#x20;

Here are the steps you need to follow. Use bookstore/public/index.bxm as a model.

1. Create a \<bx:param /> for the variable "t" at the top of the page. Default that to `manageArticles` .
2. Change the \<bx:include /> which now includes manageArticles  to include the file "#t#.bxm.&#x20;



In bookstore/management/horizontalNav.bxm

1. Change one of the \<li> in the nav to have the text "Manage Articles". Change the href property of the \<a> to open "#cgi.script\_name#?t=manageArticles".
2. Add another item in the navbar to read "Manage Books" and open "#cgi.script\_name#?t=addEdit".
3. You will need to create a page called addEdit.bxm in the bookstore/management/ folder. For now just put some dummy text in it.&#x20;
4. Make sure your site is started and open the bookstore management page. Can you use the navigation bar to switch between the Manage Articles page and Manage Books?&#x20;
