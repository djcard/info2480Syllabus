# Searching By Publisher

At this point, it is only a slight addition to search by Publisher.&#x20;

1.  Change the publisher display to be a link&#x20;

    ```boxlang
    <div>Publisher: 
         <a href="#cgi.script_name#?t=details&searchTerm=#id#">
            #bookinfo.name[1]#
         </a>
    </div>
    ```
2.  Adapt the searchBook function to search on the publisher name or id

    ````boxlang
    ```boxlang
    return queryExecute("SELECT * from books b
                   INNER JOIN publishers p
                   ON b.publisherId=p.id
                   WHERE b.title like :searchTermLIKE
                   OR b.isbn13 like :searchTerm
                   OR p.id = :searchTerm
                   OR p.name like :searchTermLIKE
                   ",
                   {
                    searchTermLike : '%arguments.searchTerm%',
                    searchTerm : '#arguments.searchTerm#'
                   }
    ```
    ````
