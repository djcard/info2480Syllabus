---
description: >-
  Goal: By the end of this document, you will have made a management index.bxm
  page and created a link to it from the public area
---

# Creating The Management Index.bxm

Later on in the course we are going to examine the rationale as to why our site is broken down the way it is but for now, we are going to forge ahead with creating some more page. The first will be the main page for the management section.&#x20;

1. Copy the `index.bxm` page from the `/public` folder and paste it into the manage folder.
2. In the browser navigate to that site by going to /bookstore/manage
3.  You will see a large missingInclude error message. This is because the page is trying to include a file called header.bxm from the same folder but that file doesn't exist. Change that reference in index.bxm to ../public/header.bxm and reload the page. You will get another error but you should see the header at the top of the page.&#x20;

    <figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>


4. Our management page is going to have a different navigation system than the public area so, for now, copy the horizontalNav.bxm file from the /public folder into the /manage folder. After doing that, in /manage/horizontalNav.bxm, change the text `Store Information` to `Manage Articles.` Reload your browser and make sure you can see the Manage Articles navigation in the top nav.&#x20;
5. We are going to adapt our /manage/index.bxm file to only have one section in our main area. Let's delete the \<section id="left">\</section>  and change the class for \<section id="center"> to `col-sm-12.`&#x20;
6. Create a new file in `/manage` called `manageArticles.bxm` . Type some text ( such as "Manage Articles" ) in the file and then change `/manage/index.bxm` to include that in the \<section id="center"> node. From now on we'll use the shorthand notation for HTML elements where # refers to an id and . refers to a class. For example, \<section id="center"> would simply be `section#center`.&#x20;
7. Adapt the footer in the same way we did the header and reference the footer.bxm in the /public folder.&#x20;
8. Your page should be opening correctly now with one exception. Do you have a broken image in your navbar? Can you open /manage/horizontalNavbar.bxm and fix that reference?
