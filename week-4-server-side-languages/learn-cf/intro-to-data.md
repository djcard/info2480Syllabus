# Intro To Data

The whole focus of this class is leading up to integrating databases with a web site. We've looked at the front end languages display the layout, colors and receives the content. We've looked at how the database stores data which can be accessed by the controller level. No matter what the langauge, they need a connection between the server side script server and the database server. Each language creates this connection in its own way. ColdFusion does it by having the server manage "datasources". Each datasource stores the location, user name, password and database name in the CF server so that when we are writing code, we can simply reference that datasource. without having to put the username and password embedded in the source code. There are plusses and minuses with that approach but it does make thing easier for us as programmers.

Everyone in the class has a unique datasource which points to their database. For example, CF has a tag called \<cfdbinfo> which allows us to connect to the database and see some of the its contents. In this case, it is set up to use your personal datasource. It matches your login name.

Here are the tables in your database dumped out. (Many of them are system tables and views. We'll get into views later)

Sorry, We couldn't show your tables because datasource \[%%SiteName%%] doesn't exist

Here are the fields in your books table dumped out:

Sorry, We couldn't show your tables because datasource \[%%SiteName%%] doesn't exist

Next week we are going to look at how to insert data into your tables programmatically and extract the data you want on demand. For the mean time, however, we're going to leave it at that.

**Exercise**: Do the test your reading quiz and then let me know that I can look at your CF pages.
