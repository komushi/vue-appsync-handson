# Create a single file to start an Apollo GraphQL API on Node Express Server

## 1. Check Node version
:warning: Make sure you have Node v9.x.x:

```
node -v
```

## 2. Create a node.js app from scratch
**Create a folder for this app**
```
mkdir graphql-express-server
cd graphql-express-server
```

**Initialize this app with all default options**
```
npm init
```

## 3. Create a single index.js
### 3-1. Reference to Express and Apollo Server libraries
```
const express = require('express');
const bodyParser = require('body-parser');
const { graphqlExpress, graphiqlExpress } = require('apollo-server-express');
const { makeExecutableSchema } = require('graphql-tools');
```

### 3-2. Add initial data
```
// Some fake data
const initBooks = [
  {
    title: "Harry Potter and the Sorcerer's stone",
    author: 'J.K. Rowling',
    gender: 'Female'
  },
  {
    title: 'Jurassic Park',
    author: 'Michael Crichton',
    gender: 'Male'
  },
];
```

### 3-3. Add Type Definitions
```
// The GraphQL schema in string form
const typeDefs = `
  type Query { 
    getAllBooks: [Book]
    getBooksByGender(gender: String): [Book]
  }
  type Book { title: String, author: String, gender: String }
`;
```

### 3-4. Add Resolvers for relative queries
```
// The resolvers
const resolvers = {
  Query: { 
    getAllBooks: () => {
      return initBooks;
    },
    getBooksByGender: function (rootObj, {gender}) {
      return [initBooks[0]];
    }
  }
};
```

### 3-5. Put together a schema
```
const schema = makeExecutableSchema({
  typeDefs,
  resolvers,
});
```

### 3-6. Add code to start Express with Apollo GraphQL and GraphiQL middleware
```
// Initialize the app
const app = express();

// The GraphQL endpoint
app.use('/graphql', bodyParser.json(), graphqlExpress({ schema }));

// GraphiQL, a visual editor for queries
app.use('/graphiql', graphiqlExpress({ endpointURL: '/graphql' }));

// Start the server
app.listen(3000, () => {
  console.log('Go to http://localhost:3000/graphiql to run queries!');
});
```

## 4. Install dependencies
```
npm install --save apollo-server-express body-parser express graphql graphql-tools
```

## 5. Start graphql-express-server and test
### 5-1. Start the Apollo GraphQL Server
```
node index.js
```

### 5-2. Visit the GraphiQL URL on browser
```
http://localhost:3000/graphiql
```

### 5-3. Run the following queries
```
query getAllBooks{
  getAllBooks {
    title
    author
    gender
  }
}
```

```
query getBooksByGender{
  getBooksByGender(gender:"Female") {
    title
    author
    gender
  } 
}
```

# Reference: 
* [graphql-express-server
](https://github.com/komushi/graphql-express-server)
