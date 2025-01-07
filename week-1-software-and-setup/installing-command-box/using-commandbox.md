# Using CommandBox

So what does CommandBox do and why are we using a command line tool when we have windows based programs so readily available? The quick answer is that it turns out that developers type a lot and frequently they have to run programs and tasks where the options are both numerous and different each time they run them. Therefore, it’s just plain faster to not have to grab a mouse, change the options and then run the task. It’s easier to just type them all. With a little practice, this will be much less foreign of a concept and you’ll find the workflow and tools you like using the most. Let’s walk through some simple activities.

#### Basic folder navigation

1. Open the Sites folder with whatever tool you normally use to browse the folders on your computer (Windows explorer, the Finder, etc) and put it side by side with CommandBox so you can see both of them. If this doesn’t work you can flip back and forth between the two windows.
2. In Command Box type “LS” and press enter. I used caps there to avoid confusion between an L and a I but lower case is fine. You should see the same list of files and folders in CommandBox as you so in your other tool. LS stands for “list”
3. In CommandBox, type “mkdir myNewExpFolder”. You should see a new folder appear in the other window. MKDIR stands for “Make Directory”.
4. This also works in reverse. Make a new folder in your GUI and when you type “ls” in CommandBox, you should see the same folder. You are looking in the same folder just using two different tools to do so.
5. In CommandBox, type “touch newFile.txt”. You created a new file called newFile.txt in that folder.
6. In CommandBox, type “cd MyNewExpFolder” and press enter. The prompt will change to say MyNewExpFolder. You are now “in” the folder MyNewExpFolder and any command you run will occur in that folder. To go “up” a level, type “cd ..”. CD stands for “change directory”.

### Downloading Packages

Package are collections of files and folders that are part of a website or program and serve a purpose. We’re going to use CommandBox to download the first set of files to get you started in this class.

1. To get started, navigate to the folder that will contain the work for this class. If you followed the example above, this will be \Sites\UML\WebDatabaseImplementation
2. Type “install uml-2480”. If you copy and paste from here, pasting into CommandBox, like every CLI, might not be as simple as CTRL-V or COMMAND-V. You will might need to right click in the CommandBox window. CommandBox will reach out to a package repository called Forgebox, find the package of software called "uml-2480" and copy it to the folder you were in when you ran the command.&#x20;
3. Type "install". and hit Enter When uml-2480 wsa copied to your hard drive, there is a file called "package.json" which has information about this particular package including **dependencies**. These are other packages which this one needs to run. If there are any, typing install will make sure they are all installed as well.&#x20;

### Starting a Server

1. Type `server start`. Wait a minute while the web server and the BoxLang server are configured. A browser will open and you’ll see the main page of a website.
2. Pay close attention to the address in the address bar. It will look something like [`http://127.0.0.1`](http://127.0.0.1)`:#####/.` This means that the page is being served off of a web server on your machine over the IP address `127.0.0.1`, which always refers to the local machine no matter what, and can be viewed over port ##### (a number). This is very important to include. If you just type in [`http://127.0.0.1`](http://127.0.0.1), you will not get this site. You might want to bookmark this address or simply remember that you can go back to CommandBox to type `server open` to open the browser again.
3. You can stop the server by typing `server stop` and enter in CommandBox from the same folder in which you started the server. This last part is important. If you type server start in a different folder, a new server will start on a different port and you will have two running at the same time. This is very handy if that is deliberate but can be confusing if it isn't.

### Configuring The Server&#x20;

In the same folder, there is a file named `server.json`  which has information about this particular server.  Since 127.0.0.1:#### can be difficult to remember, let's adapt the server configuration to use an easier to remember address. To do that we will need to run CommandBox as an administrator.

1. Close CommandBox by either typing `exit` from the prompt or clicking the `X` on the window.
2. Re

That’s it. You can read more about CommandBox in the online documentation at [https://commandbox.ortusbooks.com/](https://commandbox.ortusbooks.com/)

IMPORTANT: The installation we did with CommandBox is on YOUR computer and can not be seen by anyone else without additional configuration.&#x20;
