# Adding Permissions To The Site

## Background

As our site gets more sophisticated, we are having more and more categories of users. For example,

* Public users who are browsing and do not have an account with us
* Public users who are browsing and have an account with us
* Staff to whom we want to give special privileges such as editing the book details

What separates one person from the other, as far as the web site is concerned, is what permissions the user has. Are they known to the site? If they are known to the site, are there settings that we can build into the pages which will allow certain users access to certain parts of the site but not others? Examples could include having staff only able to access the management tools, members of a subscription service having access to a private forum, account holders being able to order special books and so on.

Permissions are usually given one of two ways – individually, where each person gets a custom set of permissions based on who they are as a person, or as a group where a group is given a set of permissions and then people are given membership to the group. Sometimes there is a mix of the two where a person’s group memberships dictate the bulk of their permissions but their permissions can be fine-tuned to a user’s particular situation.

Permissions can dictate access to an entire page, make navigation items appear or disappear or even allow certain parts of a form to appear and not others. For example, we could have had a special permission called “editISBN13” which would allow the user to edit the ISBN13 field.

For our purposes, we are going to keep this a relatively simple process and only have two levels of permission: Admin and not. If the person is an admin, they can access the management pages and tools. If they are not, they cannot, even if they are logged in.

## Steps

1. Add a field to the people table in the database called isAdmin and make it an int.
2. Make yourself an admin by putting a 1 in the isadmin field for your account.
3. In stateinfo.cfc in our obtainUser function, add `isAdmin=0` to the arguments and `isAdmin:arguments.isAdmin` to the return. Does this make sense? Check out the code base for week 8 if you need to compare your code.
4. Also the addAccount function in stateInfo.cfc, add the isAdmin field to your query. Don’t forget the SQL statement and the parameter and to default new users to 0.
5. On your navigation bar add \<cfif session.user.isadmin> \</cfif>. Put a link to the management page inside of the cfif statement.
6. If you want, as an extra precaution, add a line to the management index page that checks to see if the user is an admin. If they are not (session.user.isadmin ≠ 1), use \<cflocation> to send them to the main page. If you aren’t sure how to do that Google “cflocation adobe” and see if you can figure it out from looking at the language reference pages.
