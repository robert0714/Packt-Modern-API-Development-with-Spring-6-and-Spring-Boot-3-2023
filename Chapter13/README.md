# Chapter 13 Getting Started with GraphQL
In this chapter, you will learn about the fundamentals of **GraphQL**, including its **schema definition language** (SDL), queries, mutations, and subscriptions. The GraphQL API is popular in hand-held device-based apps such as mobile apps because it is fast and efficient in fetching the data and better than REST in certain cases. 

## Designing a schema with GraphQL tools
You can use the following tools for design and work with GraphQL, with each having its own offerings:

* **GraphiQL**: This is pronounced graphical. It is an official GraphQL Foundation project that provides the web-based GraphQL **IDE**. It makes use of **Language Server Protocol** (LSP), which uses the JSON-RPC-based protocol between the source code editor and the IDE. It is available at https://github.com/graphql/graphiql. Go to https://docs.github.com/en/graphql/overview/explorer.
* **GraphQL Playground**: This is another popular GraphQL IDE that once provided better features than GraphiQL. However, GraphiQL now has feature parity with Playground. At the time of writing, GraphQL Playground is in maintenance mode. Check out https://github.com/graphql/graphql-playground/issues/1366 for more details. It is available at https://github.com/graphql/graphql-playground.
* **GraphQL Faker**: This provides mock data for your GraphQL APIs. It is available at https://github.com/APIs-guru/graphql-faker.
* **GraphQL Editor**: This allows you to design your schema visually and then transform it into code. It is available at https://github.com/graphql-editor/graphql-editor.
* **GraphQL Voyager**: This converts your schema into interactive graphs, such as entity diagrams and all the relationships among these entities. It is available at https://github.com/APIs-guru/graphql-voyager.