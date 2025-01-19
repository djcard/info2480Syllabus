---
hidden: true
---

# Datagrip

### Background

DataGrip from Jet Brains is a higher end database manipulation tool that has a very generous student license. It has many of the same features that MSSQL Studio has but also runs on Mac and \*nix.

There are 3 steps to setting up DataGrip as your DB Tool:

1. Register for the student license
2. Download the trial software and Installing the software
3. Connecting to the class servers

### Registering for the student license

Visit [http://www.jetbrains.com/student/](http://www.jetbrains.com/student/) the click on Apply Now. Follow the directions and make sure you use your UML email address. You will be sent a license or a login which you can use as long as you’re a student.

### Downloading and Installing the Software

1. Visit [https://www.jetbrains.com/datagrip/](https://www.jetbrains.com/datagrip/) and click on download.
2. Run the downloaded exe file and follow the instructions. This can be installed anywhere.

### Connecting to the Database Servers

1. Open DataGrip and choose New Project
2. Name your new project.
3. Click on File —> Data Sources
4. In the Data Sources and Drivers window, click on the plus sign in upper left hand corner and then choose Microsoft SQL Server.
5. In the Host input type **uml-2025.cyqisqc1fx3i.us-west-2.rds.amazonaws.com** &#x20;
6. In the port input type 1433
7. In the user input put your FTPUsername
8. In the password input put your FTPPassword
9. If you see an indication to Download Missing Driver Files, do so.
10. The URL input should say something like: jdbc:sqlserver://**uml-2025.cyqisqc1fx3i.us-west-2.rds.amazonaws.com**:1433
11. Test the connection. If it works, you’re done. If not, check all the settings above for accuracy.
12. Click Ok.
13. Choose View —> Database Explorer to open the side panel
14. Expand the tree under **uml-2025.cyqisqc1fx3i.us-west-2.rds.amazonaws.com** in the left panel by clicking on the triangle then expand the dbo node.
15. You will see two nodes named table and routines.

That’s it for now
