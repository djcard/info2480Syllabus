# Personalizing Your WebSite

## Background

So far in the course we have looked at sending data from page to page via URL and form parameters and then using that data to query the database. However, our app has not had any knowledge of who the user is or if they have been there before or not. The Internet works in what is called a “stateless” condition. That means that, when a request comes in, the server gives the files, and then all connection with the user is broken. There is no continuity from one request to the next. If the site has had 100 request, it could be completely different people making the request, one person requesting the same site over and over again or a small group of people very interested in the topic.

This week we are introducing the concept of a “state”. A state is the context in which something happens. Think of statements such as a parent looking a child’s room and saying “Look what a state this room is in!” The state, in this case, is probably “messy” however, other states could be “clean”, “being cleaned” or “in process”. “He’s in a state” usually means that there is something happening to this person and they are in a bad mood, overwhelmed or some other emotion. Other states could be “normal”, “calm”, “at work”, “on a date” or something else. Notice how the conditions of a “state” change based on what we are describing. For a room, where the parent was concerned with its cleanliness, the possible states included “Clean”, “messy” and “in process”. If the room was in a house that was being constructed and the general contractor was asking for a status report, the states would probably refer to construction terms such as “framed”, “being wired”, or “complete”.

In our case, one aspect of our bookstore’s state is going to be if someone is logged in or not. Based on whether we know who the person is, we can make the page perform differently. For example, if the web site “knows” that a particular person is making a request, the system may ask for recommendations, display the user’s name or “remember” past purchases by the user.

From the technical point of view this is done through the use of 2 things. One is called a “cookie” and the other is a variable scope called the “session”. A session consists of all the visits to a web site or uses of an app by the same person (or, technically, the same browser) within a specific amount of time. In a “stateless” condition, we have what was described above - the user makes a request, the server fulfills it and then the relationship is broken. In a “stateful” situation, the system can be programmed to link all the requests together for either the user’s benefit, the system’s benefit or both.  This time frame is usually able to be set by the page unless the user set specific preference.

## This Week’s Project

We are going to add login capabilities to our web site and then adapt our site to display the name of the user while there are there. There are several steps to do this:

1. Setting up the “state” of the website.
2. Creating the data tables needed to save our users and their passwords
3. Creating a form which will allow the users to create an account.
4. Creating a form which will allow the user to login.
5. Prepping the site for some error correction so our new code won’t break
6. Adapting our code to display the name of the person throughout the site.

### Setting up the “State” of the website

If the concept of “state” is still confusing, don’t worry. It will probably make sense to you more after going through some of the exercises. Before we do anything, let’s think about the different states that we might have. For example:

The user might be **logged** in or **not logged in**

The system might know the first name of the user or might not know the first name of the user.

If we take the first item, we can make a variable called “isLoggedIn”. Since someone can’t be partially logged in, at least for what we want to accomplish, this is going to be a Boolean with the potential values of TRUE or FALSE. To start off, when the user first arrives at the site they will not be logged in. Therefore, our initial state will be that isLoggedIn=false. Since this needs to follow the user from page to page, we will put this in the session scope. Here are the steps:

1. Create a blank file called “stateinfo.cfm” in the root of your folder ( The public area)
2. Create a CFC file in the root of your folder called stateInfo.cfc. Remember that an empty component still needs to have

\`component {

}`3. At the top of stateInfo.cfm, instantiate the stateInfo component by typing`\<cfset stateFunctions = createObject(”stateInfo”) />\` 4. Under that, in the stateInfo.cfm page, add:

```
`<cfif !session.keyExists(”user”)>  
   <cfset session.user = stateFunctions.obtainUser() /> 
</cfif>` 
```

”Session” is a scope, a “bucket of variables” which is always there and to which we can read and write variables, like a structure. In this case, we are saying that if there is no “user” key in the session scope, to run stateFunctions.obtainUser and set session.user to the result.

We are going to have a structure called `user` which is going to be in the session scope. That way we will always be able to access the user’s name, account number and email if they are logged in. However, if they are not logged in, we need to have some default values. Since we are actually going to make a “clean” or empty user structure in more than one place, we’re going to make it a function that we can call from our code.\
5\. In the `stateInfo.cfc`, create a function called `obtainUser()`. It will accept 5 parameters and return a structure. The five parameters are `isLoggedIn`, `firstName`, `lastName`, `email`, and `acctNumber`. IsLoggedIn will default to false and the rest will be blank. Here is more or less what the function should look like:

```
function obtainUser(
    isLoggedIn = false,
    firstname="",
    lastname="",
    email="",
    acctNumber=""
    ) {
    return {
        isLoggedIn=arguments.isLoggedIn,
        firstname:arguments.firstname,
        lastname:arguments.lastname,
        email:arguments.email,
        acctNumber:arguments.acctNumber
    };
}
```

**Last Step:** Create a standalone page called `sessiondump.cfm` in the root of your site. In the body tag put simply:

`<cfdump var=”#session#”>`

Upload the page. Since sessions can be tricky to diagnose and keep straight, you can dump out this page at any time to see what the session variables are.

Open the page to make sure there aren’t any errors. Open sessiondump.cfm and you should see the isLoggedIn values and the session.user object with no values in it. You might also see some other keys such a CFID, CFTOKEN, sessionid and urltoken. These are session variables that CF uses to keep track of what your particular session is.

### Creating the Data Tables

There are two tables which we are going to use for these pages

1. People: Most of you should have this already made from the beginning of the course. This is the table that is going to hold our user information. This will include both visitors, staff, and book related people. This site should have the following fields as a minimum
   1. id - nvarchar(40) – Primary Key
   2. firstName – nvarchar(50)
   3. lastName – nvarchar(50)
   4. email – nvarchar(50)
2. Passwords: This table will hold the passwords for our users. It should have these fields:
   1. personId - nvarchar(40)
   2. password - nvarchar(64)

Note: If your field names don’t match exactly what is listed, that is ok. Just make the code match your field names.

### Creating our New Account and Login Page

We have a couple steps to set up our login page.

1. In our horizontalnav.cfm page, change the word “login” to a link that is going to open the same page but also pass in “p=login”
2. Create a page called login.cfm in the main folder of your web site (”/myFinalProject”)
3. Add two \<cfparam> tags with the names of “newAccountMessage” and “loginmessage”. Make both of them default to “”.
4.  On login.cfm, add a row and then split the page into two columns by using 2 divs:

    ```
    <cfparam name="AccountMessage" default="" />
    <cfparam name="LoginMessage" default="" />

    <div class="row">
        <div class="col-lg-6">Left</div>
        <div class="col-lg-6">Right</div>
    </div>
    ```

We are going to put the new user account on the left and the login screen on the right.

First, we’ll create the new user form.

1. The new user form consists of a form which includes inputs for all of the fields in the database, except the personid, and two inputs for the password. Why two? Since the password is going to be masked by dots, we want the user to have to type the password in twice to make sure that they remember it and get it right before they register it as their password. For the most part, this is a normal form. The action should be to the same page with “?p=login”. Use whatever style of form you want to use but one good option, for consistency, is the same format we used on the addEdit.cfm page in the management. All of the visible inputs should be required.
2. We are going to add a few features to our new account form to make it more user friendly but also to put some safeguards on our data. We don’t want partial or incomplete information in the database since that will do no one any good. Here are a few of the safeguards:
   1. Make all fields required
   2. Make the input for the email type=”email”. This will force the user to at least enter something with an @ in it.
   3. Make the password and confirmPassword inputs type=”password”. This will display the text in the inputs as dots instead of text and make it harder for someone to get a password over someone’s shoulder.
   4. In order to make sure that the user has correctly entered their password, let’s set it up so that they can’t submit the forms unless the password and the confirm password inputs match.

### Form Validation on the New Account Form

We really only have two requirements for the new account form.

1. Fill out all the inputs with the appropriate information. This is taken care of by the input types and the input parameter “required”.
2. Make sure that the password and confirmpassword match. This we will do with JavaScript

Javascript (JS), for the most part, runs in a browser or on a device and can be used for relatively simple tasks on the website or very complex websites using frameworks such as React, Angular or Vue.

On a webpage, JS lives inside a \<script> \</script> block. Sometimes it can be in single lines on its own but more often, JS is collected in functions or methods. We’ve looked at functions already using ColdFusion but let’s review the concept. Functions are simply a collection of code that has a name. Let me give you a real life example of what I mean. You can tell someone to:

1. examine their shoes
2. pick up one end of their shoelace in each hand
3. Cross them one over the other
4. Tuck one end under the other so they are intertwined
5. Fold one of the ends over so that it makes a loop
6. Wrap the other end of the lace around the base of the loop
7. Tuck the free end through the wrap and pull the middle though to make it’s own loop.
8. Pull tight.

OR

You can say “Tie your shoe”.

In this case “Tie Your Shoe” is shorthand or a name we give to the set of instructions that make up the “tie your shoe” activity.

We are going to make a function at the top of the login.cfm page that will check our form before we submit it. First we need to make a slight change to our form.

1. Change the input button of the new account form so it looks like this:

`<button id="newAccountButton" class="btn btn-warning" type="button" onclick=" validateNewAccount()"> Make Account </button>`

By default a \<button> tag in a form will submit the form. We don’t want to do that right away so make sure you add the type=”button” attribute.\
2\. Under the button#newAccountButton add the following:\
`<input type="submit" id="submitNewAccountForm" style="display:none" />` 3. Give your password and confirm password inputs the ids of “password” and “confirmPassword” respectively.\
4\. Above the new account form, add a div with the id#newaccountmessage. Inside this div, output the variable #newAccountMessage#. We’re going to use this to display any messages concerning problems with their choice of passwords.

What is going to happen?

The user is going to click on our button which says “Make Account”. The form is not going to submit. Instead, it is going to run a JS function at the top of the page called “validateNewAccount”. If all the criteria that we set are satisfied, this script will them click the button that will submit the form.

Make sense?

Let’s create the script that will do that.

1. At the top of the page add a \<script type=”text/javascript”>\</script> tag
2. Inside the \<script> \</script> block add the following: function validateNewAccount(){ } This is a bare bones function. It announces it is a function. It has a name which is “validateNewAccount”. Following the name are a pair of () which are required. They are for any parameters we want to pass in. We aren’t going to have any for this function. The actual function goes inside the { }.
3. Inside the function {} add the following:

`let originalPassword = document.getElementById('password').value; let confirmPassword = document.getElementById('confirmPassword').value;`

This (”let”) is the same as using \<cfset> in ColdFusion but in JS syntax. We are making two variables named originalPassword and confirmPassword. The rest of that line says what these variables’ values are.

**document** - This basically means “on this page”. When your HTML is rendered in a browser, the browser turns the page into one big object called a document. Everything on your page, including the window it is in, can be referenced by using this notation.

**getElementById(‘password’).** - This means “The Element with the id of “password”

**value** - since that element is an input, it can have a value which is the text inside the box at the time it is accessed.

What we’ve done is create two variables, one with the value of the “password” element and the other with the value of “confirmPassword” element. We did this simply because it’s easier to type “originalPassword” and “confirmPassword” and it’s easier to read.

Note: Some older browsers do not like using “let”. If yours throws an error, change “let” to “var”; 4. Now let’s do the comparison:\
\`if(originalPassword !== '' && originalPassword === confirmPassword){

} else{

}\`

This is like using \<cfif> in CF but in JS syntax. In English this is saying, “If the value in the password box is equal to the value in the confirm password box and the password box is not blank and the confirm password box is not blank, then do something. Otherwise, do something else.

Notes:

* \== is JS for equals (when used as a comparison of values). In this case 1 equals “1” even though one side is a number and the other side is a string.
* \=== compares the values AND the datatype so 1 does not equal “1” because they are different datatypes.
* && is JS for AND when stringing together conditionals like this.
* !== is JS for NOT EQUALS Make sense?

1. Now let’s fill in what we want the JS to do. If the criteria are true then do this: `document.getElementById('submitnewaccountform').click(); document.getElementById('newaccountmessage').innerHTML="";`

This is the same syntax as before: “On this page, find the element with the id of “submitNewAccountForm”, which is the invisible submit button we made, and click it”. This WILL submit the form. This in turn will have the form check all the required fields. We make the div#newAccountMessage go blank in case there are messages from failed logins there already and the form doesn’t submit yet. No need for clutter.\
2\. If the user submits the form and all of the fields are filled with correct looking data and their choice of password matches the confirm password, the form will submit and we can move on to handling the submission.

Note: JavaScript, unlike ColdFusion is CASE SENSITIVE. That means, pay attention to capital and lowercase letters.

### Handling the New User Submission

We’re going to put the mechanics of the handling the form submission in stateInfo.cfc. Since this is in the variable “stateFunctions” which is created in our stateInfo.cfm file which is always included before this component is called, it will always exists when these modules are opened. In a more complicated app, we might do this differently, but for our purposes, this will work fine.

On the login.cfm page, we’re going to check and see if our new account form has been submitted. We can do this by checking if there is a “firstname” key in the “form” scope. If there is, we are going to call stateFunctions.createNewAccount(form)

`<cfif form.keyExists("firstname")> <cfset newAccountResult = bookstoreFunctions.processNewAccount(form)/> </cfif>`

In stateInfo.cfc. the processNewAccount is going to perform 3 things

1. It’s going to check and see if this email is in our system already
2. If so, it’s going to create a new record for the user in the people table
3. and, put a record in the passwords table for the user

#### Checking if the email is unique

We need to check if the submitted email is on our system or not. The crucial issue whether or not a query returns any rows. The query would look something like this:

```
function emailisUnique(email){
    var qs = new query(datasource=application.dsource);
    qs.setSql("select * from people where email=:email");
    qs.addParam(name="email",value=arguments.email);
    return qs.execute().getResult().recordcount == 0;
}
```

Notice how the query returns a boolean ( true / false). The recordcount equals 0 or the recordcount does not equal 0. Since it returns a boolean, we can use the result of that function in an if statement.

```
function processNewAccount(formData){
    if(emailIsUnique(formData.email)){

    } else {
        return {success:false, message:"That email is already in our system. Please login"};
    }
}
```

If the email check fails, we need to let the user know that there was a problem. Notice how we’re returning a struct with two keys

* success :false
* message: “”

This tells our “view” layer whether it worked or not and what message to display to the user.

Back in login.cfm we need to handle that return. Under the call to stateFunction.processNewAccount add:

```
<cfif newAccountResult.success>
    <cfset newAccountMessage = newAccountResult.message />
<cfelse>
    <cfset newAccountMessage = newAccountResult.message />
</cfif>
```

We technically probably don’t need to put the if statement in there but if we find we need to handle the two results differently we can.

### Putting in the new account

Back in stateInfo.cfc, we need to do the first part of that IF statement - what happens if the email is unique.

First we are going to add the password to the system. Why? That might seem counterintuitive but let’s think this through. There are two queries. We need them both to work if the user is going to be able to move on. If either one fails the user can’t login. However, if the record in the people table works and the password does not, the system now thinks that the user has an account and tells the user to login. However, the user doesn’t have a password so they can’t and are effectively locked out. If we add the password record successfully but the record in the people table fails, we have an extra record in the passwords table but the user can try again.

The Password Query is a little more complicated. Not much, just a little. The biggest difference is that we don’t want to save passwords in plain text. If someone hacks our database, we don’t want them to be able to simply get everyone’s password. Don’t get me wrong, if someone is determined to get into your database and has enough time and resolve, they will do so. The trick is not to make it easy for them and therefore increase the time and effort needed to break in and decrease the value of what they are going to get when they do. To help do this second part, we are going to save the password in an encrypted format. This is called “hashing”.

A hash consists of a message, an encryption algorithm and an output which is called a digest. There are several types of hashes with varying strengths and weaknesses. The one we are going to use is called “SHA-256”. SHA stands for Secure Hash Algorithm and 256 is version being used. SHA-256 always outputs a 64-character string, no matter what size the input, and was developed by the NSA. ColdFusion has built in support for hashing and SHA-256 by using the Hash() function. For example, to hash the word “hello” the syntax is #hash(‘hello’,”SHA-256”)# and the output is 2CF24DBA5FB0A30E26E83B2AC5B9E29E1B161E5C1FA7425E73043362938B9824

The process here is that when the user submits the new user form, we take the form.password field, hash it and save the hash in the database. Then, when the user logs in via the login form, we hash their submission and compare the hash of their submission with the hash in the database. If they match, the person authenticates, if they don’t match, the password is wrong and we don’t let them in. The key feature of a hash is that the same string will hash the same way every time but even similar inputs will create vastly different outputs so you can’t “narrow down” the submission based on what the output is. It is also theoretically impossible (or at least “infeasible”) to reverse engineer the hash. Think you can make the query to insert the password based on that description? It might look something like this:

```
function addPassword(id, password){
    try {
        var qs = new query(datasource = application.dsource);
        qs.setSql("insert into passwords (personid, password) values (:personid, :password) ");
        qs.addParam(name = "personid", value = arguments.id);
        qs.addParam(name = "password", value = hash(arguments.password, "SHA-256"));
        qs.execute();
        return true;
    }
    catch(ary err){
        return false;
    }
}
```

The addPassword function returns a boolean. We’re going to use that. In the mean time, create the function to add the user’s information to the people table. Call the function “addAccount”. It should accept a uuid, firstname, lastname, email and isAdmin and insert the values into the db.

It might look like this:

```
function addAccount(
    required string id,
    required string firstName,
    required string lastName,
    required string email,
    numeric isAdmin = 0
    ) {
    var qs = new query(datasource=application.dsource);
    qs.setSql("insert into people (id, firstname, lastname, email, isAdmin) values (:personid, :firstname, :lastname, :email, :isAdmin) ");
    qs.addParam(name="personid", value=arguments.id);
    qs.addParam(name="firstname", value=arguments.firstName);
    qs.addParam(name="lastname", value=arguments.lastName);
    qs.addParam(name="email", value=arguments.email);
    qs.addParam(name="isAdmin", value=arguments.isAdmin);
    qs.execute();
}
```

#### Putting it all together

First we check if the email is unique. If that works we insert the password and if that works, we insert the people record. We return a success true or false and a message for either scenario. The processNewAccount might look like this:

```
function processNewAccount(formData){
    if(emailIsUnique(formData.email)){
        var newid = createuuid();
        if(addPassword(newid, formData.password)){
            addAccount(newid, formData.firstname, formData.lastname, formData.email);
        };
        return {success:true, message:"Account Made. Go login!"};
    } else {
        return {success:false, message:"That email is already in our system. Please login"};
    }
}
```

### Creating the Login Form

Compared to the new account form, the login form is very easy. Make a form with two inputs with the names of “loginemail” and “loginpass” and a submit button. Make the form submit to the same page with ?p=login. If the login is successful, we are going to change where the user goes but if the login fails, we are going to send them back to this login form.

Over the login form, create a div#loginmessage. We’ll use this to display messages if there is a problem with the login. Put the variable # loginmessage# in that div. Since we gave it a cfparam at the beginning of the page, that variable will always be defined, even if it is blank.

### Handling the Login Submission

We are going to handle the submission for the login in the stateinfo.cfm page, not the login page. Why is that? If the user is logged in, we want to be able to reference their name in the navigation bar by saying “Hello Joe” or “What’s Up Chuck?” or “Welcome Mary” or whatever. To do that, the session.user needs to be populated before the page gets to the nav bar. We are changing the state of the site and the sooner that is done, the more the rest of the site can access that information. Otherwise, the top part of the page thinks it’s in one state and the bottom part thinks it’s in another and chaos ensues.

In stateInfo.cfm, after the check to see if the session.user is created, create another check on whether or not form.loginPass exists.

`<cfif form.keyExists(”loginPass”)> <cfset userData = stateFunctions.logMeIn(form.loginEmail, form.loginPass) /> </cfif>`

In this case we are only looking to see if their username and password are in the database. So we have a select query:

```
function logMeIn(username, password){
    var qs = new query(datasource=application.dsource);
    qs.setSql("
        SELECT * FROM people
        INNER JOIN passwords ON people.id=passwords.personid
        WHERE email=:email and password=:password");
    qs.addParam(name="email", value=arguments.username);
    qs.addParam(name="password", value=hash(form.loginpass,"SHA-256"));
    return qs.execute().getResult();
}
```

Remember what the inner join does? In this case it joins the two tables, people and passwords and returns the rows where the id in people and the personid in passwords is the same and all the WHERE clause criteria are satisfied. Look at the “password=” in the WHERE clause. Remember we hashed the password before we saved it? Therefore, we have to hash it before we search for it. After the query we want to know if there is an account for this person or not. If so, we’ll populate the session.user with the information from the database. If not, we want to tell them to try again.

Try to create it. It might look something like this:

```
<cfif form.keyExists("loginPass")>
    <cfset userData = stateFunctions.logMeIn(form.loginuser,form.loginpass) />
    <cfif userData.recordCount == 1>
        <cfset session.user=stateFunctions.obtainUser(
            isLoggedIn=1,
            firstname=userData.firstname,
            lastname=userData.lastname,
            email=userData.email,
            isAdmin=userData.isAdmin
        ) />
        <cfset p="carousel">
    <cfelse>
        <cfset loginMessage="That login did not work." />
    </cfif>
</cfif>
```

Makes sense?

Let’s also handle the logoff process here. On the stateInfo.cfm page add:

```
<cfif url.keyExists("p") && url.p =='logoff'>
    <cfset session.user = stateFunctions.obtainUser() />
    <cfset p="carousel"/>
</cfif>
```

This says that if p=”logoff”, which it will be if they click on the logoff button we are about to make, to clear the session, set the isLoggedIn state to false and then change “p” to the carousel.

Make sense?

Only one more part for today.

### Updating the Navigation Bar to Greet the Logged in User

1. Open horizontalNav.cfm (or wherever your top navigation bar is located).
2. Find the login link you made and adapt it like this:\
   `<cfoutput> <cfif session.user.isloggedin> <li> <a>Welcome #session.user.firstname#</a> </li> <li> <a href="#cgi.SCRIPT_NAME#?p=logoff ">logout</a> </li> <cfelse> <li><a href="#cgi.SCRIPT_NAME#?p=login">Login</a> </li> </cfif> </cfoutput>`

This will display the login link if the person is not logged in and will display the user’s name and a logout link if they are logged in.

Question: Why didn’t we have to compare session.isLoggedIn to anything in our \<cfif> Statement\</cfif> i.e why didn’t we put \<cfif session.isLoggedIn eq true>? Any ideas?

Got it?

## Quick Review

A session is a collection of visits a user makes to a website or an app. We can track users to our site using sessions and cookies. The session scope in CF is a scope that follows the users around on our site. We created a new account form and did some form validation with JavaScript. We also learned about hashing which is encrypting data. After that we created a session.user which is really just a structure that contains predefined keys so we know how to access it. Throughout the whole thing we have a session variable called isLoggedIn so we can easily tell if the person has logged in or not.

And Done!
