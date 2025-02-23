---
description: >-
  Goal: By the end of this document, you'll have added a file to your repo and
  pushed the change to Github.com
---

# Pushing Changes to Github.com

1. Create a file called FirstFile.txt and put some text in it ( "Hello World" for example )
2. Save the file into your local repo ( `Sites\UML\webDatabaseImplementation\ongoingWork` ? )
3. Open your project in SourceTree and click on File Status. You should see your new file in the Unstaged Files section.&#x20;
4. Stage your file by clicking on Stage All or click on in and choose Stage Selected.
5. Enter a commit message and commit it.&#x20;
6.  Click on the PUSH icon at the top of the page&#x20;

    <figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>



IF YOU RUN IN TO SECURITY ISSUES CONTINUE ON

1. Go to Github.com and login.&#x20;
2. Click on your Avatar in the upper right and choose SETTINGS
3. Click on Developer Settings in the left hand menu
4. Expand the Personal access tokens menu on the left and choose Tokens (classic)
5. At the top, click on Generate new token (choose classic again). You might be asked to authenticate again.
6. Give your Token a name (can be anything - `general access` is perfectly fine)
7.  Select the checkbox next to repo to select all items in the repo section.&#x20;

    <figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>
8. Click on Generate Token
9. IMPORTANT: COPY THIS TOKEN TO A FILE AND KEEP IT SAFE. YOU CAN NOT ACCESS IT AGAIN AFTER YOU CLOSE THIS WINDOW AND WILL HAVE TO GENERATE A NEW TOKEN.&#x20;
10. Back in your project in Source Tree, click on Settings in the upper right
11. Under the Remotes Tab, click on the row for `orgin` then click Edit
12. In the URL / Path box, **IN FRONT OF THE EXISTING URL**, paste your token followed by an @ sign. The contents of this box will then be `token@github.com/whatever/your/site/path/is.git`
13. Click OK then OK to close all the windows.
14. Try to Push to Github again.&#x20;
15. If you are still having issues, see your instructor.&#x20;
