#Part II. Multiple API settings with Apollo GraphQL
**Multiple API settings example to start an Apollo GraphQL API on Node Express Server**

## 1. Check Node version
:warning: Make sure you have Node v9.x.x:

```
node -v
```

## 2. Clone the sample application repository
```
git clone https://github.com/komushi/apollo-express-study.git
```

**Note there are 2 API examples under apollo-express-study/graphql-api/**
**This application only start one API at a time.**
```
apollo-express-study $tree
.
├── README.MD
├── graphql-api
│   ├── books
│   │   ├── resolvers.js
│   │   └── typeDefs.js
│   └── messaging
│       ├── resolvers.js
│       ├── typeDefs.js
│       └── utils
│           ├── db.js
│           ├── db.json
│           └── upload.js
├── index.js
├── package-lock.json
└── package.json
```

## 3. Install libraries
```
cd apollo-express-study
npm install
```

## 4. Play with the "books" API
### 4-1. Edit apollo-express-study/.env
```
API_NAME=books
```

**With the settings above the application only use apollo-express-study/graphql-api/books this time.**

<pre>
apollo-express-study $tree
.
├── README.MD
├── graphql-api
│   <b>├── books</b>
│   │   <b>├── resolvers.js</b>
│   │   <b>└── typeDefs.js</b>
│   └── messaging
│       ├── resolvers.js
│       ├── typeDefs.js
│       └── utils
│           ├── db.js
│           ├── db.json
│           └── upload.js
├── index.js
├── package-lock.json
└── package.json
</pre>

### 4-2. Check the source code of the "books" API
** Note the following 2 files are almost the same from [Part I](/graphql-express-server.MD#3-create-a-single-indexjs)

**typeDefs.js**
```
module.exports = `
  type Query { 
    getAllBooks: [Book]
    getBooksByGender(gender: String): [Book]
  }
  
  type Book { 
    title: String
    author: String
    gender: String 
  }
`
```

**resolvers.js**
```
const initBooks = [
  {
    title: "Harry Potter and the Sorcerer's stone",
    author: 'J.K. Rowling',
    gender: 'F'
  },
  {
    title: 'Jurassic Park',
    author: 'Michael Crichton',
    gender: 'M'
  },
];

module.exports = {
  Query: { 
    getAllBooks: () => {
      return initBooks;
    },
    getBooksByGender: function (rootObj, {gender}) {
      return [initBooks[0]];
    }
  }
}


```


### 5-4. Stop the Node process
