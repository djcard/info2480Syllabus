# Adapting Our Management Page To Be Multi-Tool

Last week, we adapted our public facing index.bxm page to dynamically include whatever file we passed to it. This way we could display the carousel page when needed and the articles page when needed. We need to do the same thing to our management bookstore/management/index.bxm page.&#x20;

Here are the steps you need to follow. Use bookstore/public/index.bxm as a model.

1. Create a \<bx:param /> for the variable "t" at the top of the page. Default that to `manageArticles` .
2. Change the \<bx:include /> which now includes manageArticles  to include the file "#t#.bxm.&#x20;
