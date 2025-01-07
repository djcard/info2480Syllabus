---
hidden: true
---

# Testing Your Setup

Let’s make sure that you have everything set up correctly and understand what each piece of software does. Follow the directions below in order. Pay attention since some of them are designed to fail on purpose (and will say so!) to illustrate the role that a piece of software has. If at any point what you get doesn’t match what is expected, figure out why before going on to the next step. If you get all the way through, you are all set up!

1. Open up your IDE and Command Box The programs should open (this one’s pretty straightforward)&#x20;
2. In CommandBox, navigate to your ftpUserName folder (ThisIsTheRootOfTheWebSite\ftpUserName) and list the contents of that folder The listing in CommandBox should match exactly what you see in your IDE’s folder contents.&#x20;
3. 3 In your IDE, make a new folder called “InstallCheck”. You should see the folder appear&#x20;
4. 4 In CommandBox, list out the folder contents again. You should see the new InstallCheck folder&#x20;
5. 5 In CommandBox, cd into InstallCheck and make a new file called “experiment1.txt” ( “touch experiment1.txt” is the command) You should see that file appear in your IDE. You might need to refresh the listing if it doesn’t appear right away.&#x20;
6. 6 Open experiment1.txt in your IDE and type “This is my first experiment for this class”. Save it. This should save.&#x20;
7. 7 In CommandBox type “cat experiment1.txt” You should see the contents of experiment1.txt on the screen in CommandBox. Note: This is just as a double check. Most actual file manipulation will be in the friendlier IDE&#x20;
8. 8 In CommandBox, navigate back up 2 levels (cd ....) to the root of your local website (...\ThisIsTheRootOfTheWebSite). List the contents You should see your username folder in the listing. Just to make sure you’re in the right place.&#x20;
9. 9 Type “server status”. If a blank line appears or information about your server appears but is STOPPED, type “server start” and wait a moment. If the server is already running, type “server open” A browser should open with the index.cfm file showing like this:&#x20;
10. 9a Still in the browser type /ftpUserNamein the address bar (not literally ftpUserName but your username) You should see a similar page to this.&#x20;
11. 10 In your browser, bookmark the page so you have a quick link to the page. The address should be something like 127.0.0.0:#####/username. Close the tab and open the bookmark. The page will reopen to where it was with the same port. If it doesn’t, return to CommandBox and type “server open” and the browser will reopen to the right port.&#x20;
12. 11 In the browser, Navigate to /InstallCheck/experiment1.txt (or you can click on InstallCheck on the left hand side of the index.cfm page and then click on experiment1.txt) You should see the contents of experiment.txt in the browser.&#x20;
13. 12 In the IDE, make and save a new file in installcheck called experiment2.html with the following contents:
14. &#x20;In the Browser, navigate to /installcheck/experiment2.html You should see the contents of experiment2.html&#x20;
15. Open a new browser tab and go to https://comweb.uml.edu/username where username is your blackboard login You should see a page similar to the one you saw at 127.0.0.1:#####/username but with your name at the top.  You should NOT see InstallCheck in the left hand menu.&#x20;
16. Navigate to http://comweb.uml.edu/username/installcheck/experiment2.html You should get a “Page not found” or a “404” error. This is to illustrate that folder and page exist locally on your machine but NOT on the class server.&#x20;
17. FTP /installcheck/experiment2.html up to the server.&#x20;
18. Refresh the page at http://comweb.uml.edu/username/installcheck/experiment2.html You should see the contents of experiment2.html on the class servers in your space.&#x20;
19. In your IDE, create a file called experiment3.cfm (note the .cfm extension!) with the following contents: Untitled Document                                       The time is now #timeformat(now(),"h:mm tt")#            &#x20;
20. In CommandBox, list the contents of InstallCheck You should see experiment3.cfm in the listing.&#x20;
21. In the browser tab pointing to 127.0.0.1:#####/username, go to /Installcheck/experiment3.cfm You should see something like: The time is now 1:36 PM&#x20;
22. Go to https://comweb.uml.edu/ftpUserName/installcheck/experiment3.cfm You should get a Page not found or 404 error or an error display with the words “File Not Found:/username/intstallcheck/experiment3.cfm.&#x20;
23. FTP experiment3.cfm to the server and reload the browser page to http://comweb.uml.edu/username/installcheck/experiment3.cfm You should now see something like: The time is now 1:36 PM&#x20;
24. In your FTP program, view your remote site (files on the class server) and download the folder “DownloadMe”. You should see the folder appear in your IDE and in a CommandBox listing.&#x20;
25. In the Browser, navigate to “http://127.0.0.1:####/username/DownloadMe/” You should see a success page.
26. Back in CommandBox, go to the web root (\sites\uml\websiteimplementation)and type “server stop” The server should stop.&#x20;
27. Try to open /Installcheck/experiment3.cfm in the brower. You should get a server not responding or page not found error.&#x20;
28. If all of this works, you’re done! Ready for the rest of the class. Give yourself a reward of something fantastic! You enjoy the reward of something fantastic J
