---
description: >-
  Goal: By the end of this document you will have opened your project and
  started the server you made in week 1
---

# Opening our Project from Week 1 and Starting our BoxLang server

In week 1, we started a server on our local machines and opened the code which was displayed in that server in VSCode. This week we need to start the exact same server in that same folder and open the code to work on it.&#x20;

1. Open CommandBox and navigate to your folder for this class. If you followed the model in [Folder Structure](../week-1-software-and-setup/folder-structure.md), this will be `Sites\UML\WebDataImplementation.`&#x20;
2. CommandBox runs "on top of" an underlying terminal whether that is Terminal in the MAC or the CommandLine in Windows. As a result, we can send commands to that underlying terminal right from CommandBox. Type `!code .` and press enter. VSCode should open to your project.
3. Back in CommandBox, in that same folder, check the status of the server by typing server status. If to server is already running, skip step 4.&#x20;
4. type `server start`. After a moment, the server should start and your browser open.&#x20;
5. If your browser does not open, type `server open`.&#x20;

