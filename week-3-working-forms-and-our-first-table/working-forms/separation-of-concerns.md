# Separation of Concerns

The Separation of Concerns concepts simply states that we want to separate different aspects of the codebase into their own blocks or pieces of code in order to make each "chunk" of code smaller, more maintainable, reusable and secure. A concern might be the User Interface, logic which applies rules to data coming from the UI or saving or "persisting" to a file or database. An additional bonus to putting the visual aspects of as website in separate files from the logic and data is that it keeps visual developers away from accidently altering data code and keeps database developers from accidently changing a designer's visual layout or color choices.&#x20;

In BoxLang, separation of concerns can be maintained by separating our code into .bxm files  which are templates designed to appear in the browser or other user facing software and .bxs and .bx files which are scripts and classes respectively.&#x20;

For additional reading: \
\- [https://www.geeksforgeeks.org/separation-of-concerns-soc/](https://www.geeksforgeeks.org/separation-of-concerns-soc/)
