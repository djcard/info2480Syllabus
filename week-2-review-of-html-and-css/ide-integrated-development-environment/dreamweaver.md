---
hidden: true
---

# Dreamweaver

### Background

There are a few different parts to setting up Dreamweaver as your work environment. If you have not done the Getting Started activity where you create the folder structure for your project and install CommandBox, do so before continuing.

* Planning your setup.
* Downloading all of the software off of the Internet.
* Installing Dreamweaver.

Ready to get started?

## Planning Your Setup

Read through this guide first. You are welcome to deviate from this process if you already have a good handle on how you want your system set up but following these directions will make sure that you have everything set up for this course.

**Notes**:   All instructions are written for a Windows Environment

If you already have Dreamweaver set up for another class or for work, you are welcome to use that installation. You don’t need to have a separate install for this class but you will need to set up a separate site for this class.

### Downloading Dreamweaver

Since Dreamweaver is a commercial product there are many different ways to legally obtain it. This can include from the UML bookstore or software sites or from [Adobe.com](http://adobe.com). [Adobe.com](http://adobe.com) also has moved to a subscription service for much of it software which means you can obtain the software you need to use and pay a subscription fee each month rather than the hundreds of dollars up front. For more information visit [https://creative.adobe.com/plans](https://creative.adobe.com/plans).

## Creating a Site in Dreamweaver

1. Open up Dreamweaver
2. Click on SITE —> New Site
3. On the left side of the window which appears, click on Site
   1. The Site name can be WebDataImplementation
   2. Choose your folder as the Local Site Folder (sites\uml\WebDataImplementation\ThisIsTheRootOfTheWebSite\ftpUserName)
   3. Leave the Git information blank. If you are curious about Git, ask during chat.
4. Click on Server
   1. Click on the + sign to create a new server connection
   2. Server Name: Comweb
   3. Connect using: FTP over SSL/TLS (implicit encryption)
   4. FTP Address: [Comweb.uml.edu](http://comweb.uml.edu)
   5. PORT: 990
   6. Enter your username and password
   7. Root Directory: /ftpUserName
   8. Web URL: [http://comweb.uml.edu/](http://comweb.uml.edu/)
   9. Authentication: Trusted Server
   10. More options: Check Passive mode
   11. More options: Check Use IPV6 Transfer Mode
   12. Click on Test and you should connect
5. Click on the icon which is all the way to the right on the same row as the Manage Sites dropdown menu. This expands the window so you can see both the local files (on the right) and the remote files (on the left).
6. Click the icon (right next to the Manage Sites Drop Down Menu to connect to the remote server.
7. The process of editing and creating your web sites involves using the up and down icons: . The down arrow moves selected files from the server to your local hard drive (i.e. downloads). The up arrow moves selected files from your local hard drive to the server (i.e. uploads. I’m sure you see the pattern by now). A typical work flow would be to open a file, edit it, look at it on your local server or upload it to the school server and view it.
