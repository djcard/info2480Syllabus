---
description: >-
  Goal: By the end of this document you will have branched off of the master
  branch, edited the MyFirstText.txt file and then merged it back into the
  master branch.
---

# Making Changes and Merging them

[Watch Video](https://youtu.be/lnEJLzNkCjk)

Let's make some edits. Remember, we don't want to edit our Master version. We want to make our edits in a copy and then, when we are happy with them, merge them into our main branch.&#x20;

1. In SourceTree, double click on the "master" branch in the left side menu under Branches to ensure it is checked out (it will appear in bold if it is) .
2. At the top of the screen, click on BRANCH and name your branch "First-Edit" in the window that pops up. \
   ![](<../../.gitbook/assets/image (3) (1) (1) (1).png>)\
   \
   ![](<../../.gitbook/assets/image (5) (1) (1) (1).png>)
3. Click on Create Branch.
4. You will see First-Edit appear in the side menu under branches and will be in bold to indicate that it is the one checked out.&#x20;
5. Open MyFirstText.txt in a text editor. If you still have it open from before, you do not need to close and re-open it.&#x20;
6. Make some changes to it. These can be anything but here is an example:\
   ![](<../../.gitbook/assets/image (6) (1) (1).png>)
7. Save it and go back to SourceTree. Click on File Status again and you will see your file in the Unstaged Files area\
   ![](<../../.gitbook/assets/image (7) (1) (1).png>)
8. Click on it and in the upper right, will see something like this:\
   ![](<../../.gitbook/assets/image (8).png>)\
   This shows the changes which have been made in the file. The lines highlighted in red have been deleted or changed. The green lines have been added. Does this line up with the changes you made?
9. Stage the changes by clicking on Stage Selected like you did before.&#x20;
10. Enter a comment in the box on the bottom and click on Commit. You've now put the changes into the First-Edit branch in your repo.&#x20;
11. Close the file in your text editor.&#x20;
12. Back in SourceTree, if you want to see your original file, double click on "master" and then open MyFirstText.txt in your text editor. See the original? Close that. Double click on FIrst-Edit and open the file again. See the changes?&#x20;

## Merging Your Changes Into the Master Branch

1. Check out the master branch by double clicking on "`master`" in the left hand menu. Make sure it is in bold to indicate it is checked out.&#x20;
2. Right click on First-Edit and choose "`Merge First Edit into current branch`".&#x20;
3. Confirm the merge by clicking ok.&#x20;
4. Open MyFirstText.txt in your text editor. It should have all of your changes in it.&#x20;
