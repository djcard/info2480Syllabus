# Using CommandBox

So what does CommandBox do and why are we using a command line tool when we have windows based programs so readily available? The quick answer is that it turns out that developers type a lot and frequently they have to run programs and tasks where the options are both numerous and different each time they run them. Therefore, it’s just plain faster to not have to grab a mouse, change the options and then run the task. It’s easier to just type them all. With a little practice, this will be much less foreign of a concept and you’ll find the workflow and tools you like using the most. Let’s walk through some simple activities.

#### Basic folder navigation

1. Open the Sites folder with whatever tool you normally use to browse the folders on your computer (windows explorer, the Finder, etc) and put it side by side with CommandBox so you can see both of them. If this doesn’t work you can flip back and forth between the two windows.
2. In Command Box type “LS” and press enter. I used caps there to avoid confusion between an L and a I but lower case is fine. You should see the same list of files and folders in CommandBox as you so in your other tool. LS stands for “list”
3. In CommandBox, type “mkdir myNewExpFolder”. You should see a new folder appear in the other window. MKDIR stands for “Make Directory”.
4. This also works in reverse. Make a new folder in your GUI and when you type “ls” in CommandBox, you should see the same folder. You are looking in the same folder just using two different tools to do so.
5. In CommandBox, type “touch newFile.txt”. You created a new file called newFile.txt in that folder.
6. In CommandBox, type “cd MyNewExpFolder” and press enter. The prompt will change to say MyNewExpFolder. You are now “in” the folder MyNewExpFolder and any command you run will occur in that folder. To go “up” a level, type “cd ..”. CD stands for “change directory”.

### Downloading Packages

Package are collections of files and folders that are part of a website or program and serve a purpose. We’re going to use CommandBox to download the first set of files to get you started in this class.

1. To get started, navigate to the folder that will be the “top” of your website for this class. If you followed the example above, this will be \Sites\UML\WebDatabaseImplementation
2. Type “install git://github.com/djcard/UMLInfo2480.git”. If you copy and paste from here, pasting into CommandBox (like every CLI might not be as simple as CTRL-V or COMMAND-V. You will might need to right click in the CommandBox window. I know, kind of destroys the type only motif. Trust me, it bugs everyone.)
3. When the package is done installing, type ls to see the new contents. You’ll see a folder called ThisIsTheRootOfTheWebsite.
4. CD into this folder. `cd ThisIsTheRootOfTheWebSite`
5. Type “server start”. Wait a minute while the web server and the CF server are configured. A browser will open and you’ll see a screen that looks like this:
6. Pay close attention to the address in the address bar. It will look something like[http://127.0.0.1](http://127.0.0.1):#####/. This means that the page is being served off of a web server on your machine over the IP address 127.0.0.1, which always refers to the local machine no matter what, and can be viewed over port ##### (a number). This is very important to include. If you just type in[http://127.0.0.1](http://127.0.0.1), you will not get this site. You might want to bookmark this address or simply remember that you can go back to CommandBox to type “server open” to open the browser again.
7. You can stop the server by typing “server stop”.
8. You can start it again by going to the same folder and typing “server start”. If you go to a different folder, you will start a different server pointing to a different set of files. This is very handy if you have multiple web pages you want to open locally but frustrating if you want to just get to a particular project.
9. The last step is to rename the folder called “renameToYourFolder” to your ftpUserName. For example, renameToYourFolder —> dcard62886. You can do this by typing `rename renameToYourFolder dcard62886` or whatever your ftpUserName is.

That’s it. You can read more about CommandBox in the online documentation at [https://ortus.gitbooks.io/commandbox-documentation/content/](https://ortus.gitbooks.io/commandbox-documentation/content/).

IMPORTANT: The installation we did with CommandBox is on YOUR computer. The connection at[http://comweb.uml.edu/ftpU\*serName\*](http://comweb.uml.edu/ftpU\*serName\*) is on a computer located at the school. They are not the same thing. The site at 127.0.0.1 is yours and yours alone. For anything to be viewed by me or the class it must be uploaded to the server via the FTP process which we will set up in a future document. This is VERY IMPORTANT to realize. I can’t see what is at 127.0.0.1. Only what is at[http://comweb.uml.edu/ftpU\*serName](http://comweb.uml.edu/ftpU\*serName).\*
