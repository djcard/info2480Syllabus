# Configuring Our Site To Use Our Database

Just like we configured MySQL Workbench to connect to our database, we need to configure our BoxLang server to connect to it as well.

1. Open your ongoingWork folder in VSCode.
2. In the file menu on the left side, find the file called .cfconfig.json. This is a special configuration file that CommandBox feeds into our BoxLang server when it starts up. In it we can define datasources, mapped drives and a number of other settings.&#x20;
3. Notice how in the .cfconfig.json file, there is a section called datasources![](<../../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png>)
4. Replace where it says \*\*DSOURCENAME\*\* with your username ( first\_last ). ![](<../../.gitbook/assets/image (5) (1).png>)
5. Notice the other values which are in a format like ${}? These are for server names, usernames and passwords BUT you don't want to check those values into a git repo because you don't want them shared. So what does that format mean? Those values are being pulled from another file called `.env`  which does not get checked into the git repo.&#x20;
6. Open up the `.env` file.
7.  Put the appropriate values into the .env file and save it. Something like this but with your values:&#x20;

    <figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
8.  The last step is to open the file Application.bx and add the line this.datasource  = 'Username' where Username is the username I sent your, not the actual word username.&#x20;

    <figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
9. In CommandBox, in your ongoingWork folder, restart your server by typing `server restart`.
