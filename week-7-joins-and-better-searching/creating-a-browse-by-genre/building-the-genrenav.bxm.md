# Building the GenreNav.bxm

We already created our distinct genres query. All we need to do it call it and display the results

1. Create a reference to bookstore.common.books\
   \<bx:set common = createObject("bookstore.common.books") />
2. Create a variable and then call the common.distinctGenres method.
3. In the current genreNav.bxm, replace the hardcoded \<li> tags with a loop over something like this: `<li class="nav-item">`\
   &#x20;    `<a class="nav-link" href="#cgi.SCRIPT_NAME#?t=details&genre=#genreid#">`\
   &#x20;         `#genrename#`\
   &#x20;    `</a>`\
   &#x20;`</li>`

Notice how they open our existing details.cfm module but pass in a new variable called “genre”. Don’t forget to wrap the loop in a \<bx:output>\</bx:output>
