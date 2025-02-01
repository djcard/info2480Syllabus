---
description: >-
  Goal: By the end of this document, you will have created a git repository,
  created a new file, staged the file and committed it to your local repo.
---

# Creating a Local Repository

Once you have installed SourceTree (or other client) you are ready to experiment with git. The first step is to create a git repo. We are going to use SourceTree to perform all of these actions for now.&#x20;

[View Video](https://youtu.be/7i54Sd5IIww)

## Creating a Git Repository

1. Open SourceTree and click the + symbol in top menu bar or choose `FILE -> Clone/New` in the tool bar.&#x20;
2. Click on CREATE in the tool bar that appears\
   &#x20;![](<../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png>)
3. If you followed the pattern outlines in the [Folder Structure](../folder-structure.md) section, navigate to `Sites\UML\WebDataImplementation\`and make a new folder called `"practiceGit"` If you didn't, simply choose a empty folder.   \
   ![](<../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)
4. Click Create.&#x20;
5. Use either Windows Explorer or Finder to go to the `practiceGit` folder. Make sure you have it configured to see hidden files and folders ( Google how if you need to). You should see a folder called ".git" folder. This is where git will save all the information it needs to manage all the branches for the repository ( or repo ) in this folder. **Note: DO NOT SAVE ANY FILES IN THAT FOLDER. Also, do not edit any of the files in that folder. Bad things to your work can happen. Let git handle it all.**&#x20;

## Creating, Staging and Committing Files

1. Open a text editor (like Notepad or TextEdit. Do **Not** use Microsoft Word or Pages. In TextEdit, make sure you choose `FORMAT -> make Text File` if necessary) and create a new file called "MyFirstText.txt" in your git1 folder.&#x20;
2. Type "This is my first file with git. So far so good." and then save into that `practiceGit` folder.  This saves the file onto your hard drive but it is NOT in your git repository yet.&#x20;
3. Go back to SourceTree and click on the "`practiceGit`" tab. If you closed that tab, click on the + sign again and use ADD to open that repo again.&#x20;
4. In the left hand menu pane, under WORKSPACE, click on FILE STATUS.&#x20;
5. In the lower half of the center column you should see a section called "UNSTAGED FILES" and in it your MyFirstText.txt file should be listed. Click on it.&#x20;
6. You should see the contents of your file appear in the upper right.&#x20;
7. Back in the center column, click on "STAGE SELECTED" (On Mac: right click and choose `Stage Files` ). This will move MyFirstText.txt from the unstaged area to the STAGED FILES area. This area is a list of all the files which are going to be put into your repo but are not there yet.&#x20;
8. At the bottom of the screen you will see a text box with the button COMMIT underneath it. In the text area, type "INITIAL COMMIT". It is customary to put a comment describing the work you did for each commit.&#x20;
9. Click Commit. This will put your file into the git repository in that folder. It is now in the version control system and managed by git.&#x20;
10. Look in the left menu panel under BRANCHES and notice that one called "master" has been created. It is in bold which means that is the branch which is currently checked out so all the files, no matter what program in which you open then, will be editing the files in this branch. \
    ![](<../../.gitbook/assets/image (2) (1) (1) (1) (1).png>)



