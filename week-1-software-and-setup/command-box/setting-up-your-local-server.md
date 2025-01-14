---
description: >-
  Goal: By the end of this document you'll have started a web server and BoxLang
  scripting engine on your local machine.
---

# Setting Up Your Local Server

## Starting a Server

1. From Commandbox and inside the `ongoingWork` folder, type `server start`. Wait a minute while the web server and the BoxLang server are configured. A browser will open and you’ll see the main page of a website.
2. Pay close attention to the address in the address bar. It will look something like [`http://127.0.0.1`](http://127.0.0.1)`:#####/.` This means that the page is being served off of a web server on your machine over the IP address `127.0.0.1`, which always refers to the local machine no matter what, and can be viewed over port ##### (a number). This is very important to include. If you just type in [`http://127.0.0.1`](http://127.0.0.1), you will not get this site. You might want to bookmark this address or simply remember that you can go back to CommandBox to type `server open` to open the browser again.
3. You can stop the server by typing `server stop` and enter in CommandBox from the same folder in which you started the server. This last part is important. If you type server start in a different folder, a new server will start on a different port and you will have two running at the same time. This is very handy if done deliberately but can be confusing if it isn't.

## Configuring The Server&#x20;

In the same folder, there is a file named `server.json`  which has information about this particular server.  Since 127.0.0.1:#### can be difficult to remember, let's adapt the server configuration to use an easier to remember address. To do that we will need to run CommandBox as an administrator.

1. Close CommandBox by either typing `exit` from the prompt or clicking the `X` on the window.
2. Re-open CommandBox but this time, do it running as the Administrator. On Windows, right click on the box.exe file and choose `Run As Administrator`. On a Mac, this might mean opening terminal, navigating to where you unzipped the box application and then typing `sudo box` . You might need to install your Admin password after doing that.
3. We need to install another package that is actually for CommandBox itself, not our app specifically. Type `install commandbox-hostupdater`.&#x20;
4. Once that installs we are going to make some settings changes. Think of a domain name that you'll remember like `webclass.local` or something like that. It can literally be anything. I just use the `.local` to remind myself that it is on my computer and not on the web. Type `server set web.host=webclass.local`. Then type `server restart`. If you get an error, try `server restart` again. Sometimes the hostupdater needs to navigate some permissions and it errors.
5. Once the server restarts, type `server open` to open the browser to the new address. It should say `webclass.local:######`.  We've changed the address in the nav bar, but not the port.
6. Go back to CommandBox and type `server set web.http.port=80` and type `server restart` then `server open` after the server restarts. You should see webclass.local in the address bar.&#x20;
7. If you are done working on this for now, type `server stop`.&#x20;

That’s it. You can read more about CommandBox in the online documentation at [https://commandbox.ortusbooks.com/](https://commandbox.ortusbooks.com/)

IMPORTANT: The installation we did with CommandBox is on YOUR computer and can not be seen by anyone else without additional configuration.&#x20;
