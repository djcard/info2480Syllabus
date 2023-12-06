# IntelliJ

### Background

IntelliJ from Jet Brains is a higher end development environment that has a very generous student license.

There are 5 steps to setting up IntelliJ as your IDE:

1. Register for the student license
2. Download the trial software and Installing the software
3. Creating a project for your website
4. Connecting to the class servers
5. Uploading and Manipulating Files

### Notice

It is essential that you set up the new VPN BEFORE doing the instructions in document. Please refer to the Getting Started document or visit [https://www.uml.edu/it/services/get-connected/remote-access/](https://www.uml.edu/it/services/get-connected/remote-access/) for more information.

### Registering for the student license

Visit [http://www.jetbrains.com/student/](http://www.jetbrains.com/student/) the click on Apply Now. Follow the directions and make sure you use your UML email address. You will be sent a license or a login which you can use as long as you’re a student.

## Installing IntelliJ

### Downloading the Software

1. Visit [https://www.jetbrains.com/idea/](https://www.jetbrains.com/idea/) and click on download. Choose the Ultimate version.

### Installing the software

1. Run the downloaded exe file and follow the instructions. This can be installed anywhere.

## Creating a project

Projects are made up of all the files that go into make a final product. For some languages this can include all sorts of libraries, dependencies, modules, outside programming and more. However, for our purposes, we are not using any of those so the process is very straightforward.

1. Click on File —> Open
2. Navigate to the root of your website. This is the _ftpUserName_ folder inside of the ThisIsTheRootOfTheWebsite folder.
3. Click Finish. If asked, open the project in a new window.

### Connecting to the Class Servers

IntelliJ has a built in tool called Deployment which we’ll use to connect to the UML servers.

1. Click on TOOLS —> Deployment —> Configuration
2. On the Connections Tab, change the type to “FTPS”
3. The FTPs Host is [comweb.uml.edu](http://comweb.uml.edu)
4. The port is 990
5. Under the advanced area choose TLS: Implicit
6. Under the advanced area choose Passive mode
7. The root path is / \*\*You can also click on Autodetect to fill this in for you. -
8. Enter your ftpUserName and password - Check Save Password - -
9. Enter the web server URL as[http://comweb.uml.edu](http://comweb.uml.edu)
10. Under the Mappings tab, the local path should be your ftpUserName folder
11. The Deployment Path should be /
12. The web path on the server should be /
13. Go back to the Connection tab and click on Test FTPS Connection
14. You should see a window that says Successfully connected to [comweb.uml.edu](http://comweb.uml.edu)

## Uploading and Downloading Files

On the left hand side of the screen you should see a list of the files in your local folder. By right clicking on a folder or file and going to the Deployment Menu you can:

* Upload the file to Comweb
* Download the files from Comweb
* Compare the Deployed Version on Comweb
* Sync the Deployed with Comweb (this is a bit dicy when it comes to version so perhaps best to be avoided).

We’ll be doing more with uploading and downloading in a later document.
