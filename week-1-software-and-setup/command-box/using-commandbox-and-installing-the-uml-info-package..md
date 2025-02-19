# Using CommandBox And Installing the UML-Info package.

So what does CommandBox do and why are we using a command line tool when we have windows based programs so readily available? The quick answer is that it turns out that developers type a lot and frequently they have to run programs and tasks where the options are both numerous and different each time they run them. Therefore, it’s just plain faster to not have to grab a mouse, change the options and then run the task. It’s easier to just type them all. With a little practice, this will be much less foreign of a concept and you’ll find the workflow and tools you like using the most. Let’s walk through some simple activities.

## Basic folder navigation

1. Open the Sites folder with whatever tool you normally use to browse the folders on your computer (Windows explorer, the Finder, etc) and put it side by side with CommandBox so you can see both of them. If this doesn’t work you can flip back and forth between the two windows.
2. In Command Box type “LS” and press enter. I used caps there to avoid confusion between an L and a I but lower case is fine. You should see the same list of files and folders in CommandBox as you so in your other tool. LS stands for “list”
3. In CommandBox, type “`mkdir myNewExpFolder`”. You should see a new folder appear in the other window. MKDIR stands for “Make Directory”.
4. This also works in reverse. Make a new folder in your GUI and when you type “ls” in CommandBox, you should see the same folder. You are looking in the same folder just using two different tools to do so.
5. In CommandBox, type “touch newFile.txt”. You created a new file called newFile.txt in that folder.
6. In CommandBox, type “cd MyNewExpFolder” and press enter. The prompt will change to say MyNewExpFolder. You are now “in” the folder MyNewExpFolder and any command you run will occur in that folder. To go “up” a level, type “cd ..”. CD stands for “change directory”.

## Downloading Packages

Package are collections of files and folders that are part of a website or program and serve a purpose. We’re going to use CommandBox to download the first set of files to get you started in this class.

1. To get started, navigate to the folder that will contain the work for this class. If you followed the example in the [Folder Structure](../folder-structure.md) section, this will be `\Sites\UML\WebDatabaseImplementation\ongoingWork`&#x20;
2. Type `install uml-2480`. If you copy and paste from here, pasting into CommandBox, like every CLI, might not be as simple as CTRL-V or COMMAND-V. You will might need to right click in the CommandBox window. CommandBox will reach out to a package repository called Forgebox, find the package of software called `uml-2480` and copy it to the folder you were in when you ran the command.&#x20;
3. Type `LS` again and you will see files in what was an empty folder. If you run this command again, the files that are here now will be overwritten so careful if you make edits to them that you don't run it again by accident. Many times packages are installed in a sub folder to avoid that kind of problem but our package is meant to be the root of your class website so it is configured to install at the root level.&#x20;

## **Committing these changes to Github.com**

1. Navigate back to your class project in SourceTree.&#x20;
2. Click on File Status in the left hand folder.&#x20;
3.  **IMPORTANT**: In the Unstaged files area, right click on the file .env and choose Ignore. In the popup choose `ignore exact filename(s)` and click OK.

    <figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

    A .env file is a way of storing secure passwords locally on your machine and is NOT meant to be checked into a repo.&#x20;
4. Once you have ignored .env, a new file called .gitignore will be created and .env will be added to it.&#x20;
5.  Click on Stage All  to move all the files to the Staged files area.&#x20;

    <figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>
6. Add a comment ( i.e. Class Files Commit ) and Commit the files.&#x20;
7.  Click on PUSH to push the files to Github.

    <figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>



That’s it. You can read more about CommandBox in the online documentation at [https://commandbox.ortusbooks.com/](https://commandbox.ortusbooks.com/)

IMPORTANT: The installation we did with CommandBox is on YOUR computer and can not be seen by anyone else without additional configuration.&#x20;
