# Connecting Your Local Environment To The School DB Server

### Background

The main purpose of integrating a tool like CommandBox into your development environment is to very easily run a web server and ColdFusion server on your local machine. This gets rid of the need to upload every revision to the school server to see the result of your work. That works when all we are working with is HTML/CSS/JS or if our ColdFusion only needs to talk to the files on our local computer. However, now that we are getting into using more data driven operations, we need to either put a database on our local machine or connect the ColdFusion server to the database on the UML computer. The latter is much easier so we are going to do that for now.

When writing a \<cfquery> in CF there are two attributes that are needed. The first is the name of the query and the second is the datasource.

Tag:

\<cfquery name=”myQuery” datasource=”MyDatasource”>

SQL

\</cfquery>

Script

var myQuery = new query(datasource=”MyDatasource”);

myQuery.setSql(SQL);

var results = myQuery.execute().getResult()

The Datasource is the name of the connection that CF will use to submit SQL to the database server and get the results back. This is similar to when we set up MSSQL Studio or DataGrip to connect to the UML servers. We told the program what address, port, database, username and password to use and it connected. We are going to do the same thing with the CF server on your computer.

## Setting the Datasource Variable

In the root of your personal folder on the comweb server or in the commandBox folder on your local machine there is a file called Application.cfc. On the comweb server, you shouldn’t have to touch it. In your commandBox installation, there are a few locations which have the value “%%SiteName%%”. Replace everywhere “%%SiteName%%” with your foldername. At the very least there should be a line saying:

\<cfset this.dsource=”_username_”> near the top of the file and \<cfset application.dsource=”_username_”> inside a function called onApplicationStart.

## Steps to Connect CF to the UML Database.

1. In CommandBox, navigate to folder with your website in it and type “server start” to launch the web server and to open the browser. Note: I’ve noticed a weird bug at times so if the server doesn’t start and the browser doesn’t open, try typing “server start cfengine=lucee” which will work around that issue.
2. After the browser opens, look in the lower right corner of your screen, in the system tray, you will see an icon which looks like this on Windows. . On a Mac it will appear in the upper right. Click on the icon to open the help menu. If you have multiple servers running, the name of the server will correspond to the folder in which it started.
3. In the menu that comes up, choose either Open Server Admin or Open Web Admin. The directions here will correspond to the server admin but either is fine.
4. The first time you follow these directions, you will see a screen which says that a password has not been set. If so, set the password like this:
   1. Back on the System Tray Icon, choose OPEN —> SERVER HOME. A window pointing to a folder will appear.
   2. Drill down to WEB-INF/lucee-server/context.
   3. Create a text file called password.txt
   4. Open it and on the first line, type in what you want the Admin Password to be.
   5. Save the text file.
   6. Go back to the browser and click on IMPORT FILE button.
   7. Go login using that password.
5. In the admin window, click on DataSource on the left side
6. In the following form, put whatever name you want (although you might want to stick to your db login name just to be consistent) into the Name field and change the Type to Microsoft SQL Server.
7. In the following screen fill in
   1. Host: [comweb.uml.edu](http://comweb.uml.edu)
   2. Database: the name of your database
   3. Port: 51433
   4. Username: your username
   5. Password: your password
   6. Verify Connection: checked
   7. Click Create
8. If the Check column in the following screen is OK then you are all set. If not, then check the settings and try again.

From then on, you can use the name of that data source in your cfquery tags and get the data out of your database on the school servers.
