# gql Notes

GraphQL is like a query language for API's. Like how SQL is DSL for RDMSs, Graphql is for APIs.

- Problem Solved by GraphQL:
  - Less number of AJAX calls from client to server or other endpoints
  - Client doesn't know anything about underlying endpoints and thinks Graphql route/endpoint is its source
  - Thinner server can be developed
  - Development can be faster, front-end folks don't need depend too heavily on the backend folks, if and only if backend folk don't change the under lying API too much
  - Only the data requested is sent! No need to pick and choose things you want from a giant set of data

- Data is saved/represented in the form of a graph, where in edges determine relations... like a Social Network
  - Getting the data is via trversal of edges

- GraphQL is used as a middleware. It needs a schema to function properly. Basically what every single object would look like just like DBSchemas
  - A _rootQuery_ is what determines the entry point into the graph