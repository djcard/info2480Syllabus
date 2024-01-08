# Making a Forgot Password Page

## Background

In an ideal world, users and staff would never forget their passwords and this wouldn’t be an issue. However, in the real world, people forget their passwords all the time and they need to be reset. At that point, what does the website do? Does it allow them to change it themselves or does it force them to call IT support? Again, practically, there is no way that IT can reset thousands if not millions of users’ passwords so it is good to have a “forgot password” link.

However, this faces a new dilemma. The purpose of a password is to make sure the user is who they say they are. How do we make sure that the person asking for their password to be reset is the owner of that account?  There are typically three methods:

1. Security Questions – This basically boils down to some other user volunteered information that the website has on file that they can use to authenticate the user and verify their identity. Essentially this acts like an alternate password.
2. Communicating with an alternative account such as emailing a link or texting a code – This shifts the burden of verifying the user to the email provider. The idea is that if the user can access that email account or is in physical possession of the users’ phone or other device, they must be who they claim to be.
3. Using a built in device such as fingerprint reader or eye scanner – This is both the most secure and the most expensive, in money, time and effort. However, more and more, this is appearing in daily life and in consumer devices. Many if not most, phones have fingerprint or facial recognition built into the operating system.

We are not going to use such high end techniques, not because they are out of reach or massively complicated to implement but simply time and focus. The class is on web based database systems, not on website security per se although they are very much linked.

Instead, we are going to make the user submit their last name and email address as a substitute for a security question and, if both the last name and the email address match, we will allow them to view the reset password form.

By now, you should be able to piece together they steps to create this process. Consequently, I will list the steps below but not give detailed instructions.

## Steps

* On the login form, create a link labelled “forgot password” which opens a “forgot password” module in the center part of the public page.
* Present a form which asks for the last name and email address of the user.
* When they form is submitted, check the database to see if the last name and email address match an existing account. If it does, allow them to see a “change password” form. If it does not, display a message saying that there is no account which matches that information.
* The reset form makes the user type their password twice and checks to make sure they are the same. If it is the same, it submits and saves the new password encrypted.
* The user can then log in with the new password.
* One new item which I’ll touch on is a new tag called \<cflocation> this sends the user to a new page as in \<cflocation url=”[http://www.redsox.com](http://www.redsox.com)” />. Can you think of a use for this in this instance?

Make sense? We have done all of these techniques already in the class. If you need to, find the older documents or look at your current code to find out where.
