# MSSQL Studio

### Notice

It is essential that you set up the new VPN BEFORE doing the instructions in document. Please refer to the Getting Started document or visit [https://www.uml.edu/it/services/get-connected/remote-access/](https://www.uml.edu/it/services/get-connected/remote-access/) for more information.

## Downloading SQL Studio

URL:[https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)

* Go to the URL above and click on the Download SQL Management Studio 18.12.1 link.
* Save the Files you download to the DOWNLOADS folder you made in above.
* Done Downloading for now! Take a Break!

### Installing SQL Management Studio

SQL Studio is the program we will use to manage the databases we create in MSSQL.

* Navigate to the file you downloaded earlier.
* Double Click on the file to start the installation.
* Follow the installation directions.

### Connecting to SQL Server

* Open SQL Management Studio
* If the Connect To Server Window does not open, choose FILE —> CONNECT OBJECT EXPLORER
* The Server name is [comweb.uml.edu](http://comweb.uml.edu) and your Login is your ftpUserName. The port is 51433 which, for SQL Studio, is put next to the URL separated by a **comma**. This is only needed in SQL STUDIO. Other programs will probably allow you to change the port using other means.

Figure 1: Settings for connecting to SQL Server

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/33764043-8d28-4a24-9987-f366a041f6fe/Untitled.png)

* Once the Management Studio connects you will see a DB named after you in the left hand pane. For now, just leave it alone until we get to that point in the course.
