# Part IV. Create Vue.js application & AppSync backend manually

**Use AWS management console to create AppSync API**

**Use vue-cli-plugin-appsync to generate a Vue.js application**

## 1. Manually Setup AWS AppSync (GraphQL API Server Side) with AWS management console

### 1-1. Default GraphQL API
```
type Query { 
    getAllBooks: [Book]
}

type Book { 
    title: String!
    gender: Gender
    author: String
}

enum Gender {
    Male
    Female
}

schema {
    query: Query
}
```

### 1-2. Create a DynamoDB Resource 
**Click the "Create Resouces" button**
* Select a type: Book
* Table name: BookTable
* Primary Key: title
* Sort Key: None
* Additional Indexes: None

### 1-3. Manually update CreateBookInput and UpdateBookInput for gender (enum type)
```
type Book {
  title: String!
  gender: Gender
  author: String
}

type BookConnection {
  items: [Book]
  nextToken: String
}

input CreateBookInput {
  title: String!
  author: String
  gender: Gender
}

input DeleteBookInput {
  title: String!
}

enum Gender {
  Male
  Female
}

type Mutation {
  createBook(input: CreateBookInput!): Book
  updateBook(input: UpdateBookInput!): Book
  deleteBook(input: DeleteBookInput!): Book
}

type Query {
  getAllBooks: [Book]
  getBook(title: String!): Book
  listBooks(first: Int, after: String): BookConnection
}

type Subscription {
  onCreateBook(title: String, author: String): Book
    @aws_subscribe(mutations: ["createBook"])
  onUpdateBook(title: String, author: String): Book
    @aws_subscribe(mutations: ["updateBook"])
  onDeleteBook(title: String, author: String): Book
    @aws_subscribe(mutations: ["deleteBook"])
}

input UpdateBookInput {
  title: String!
  author: String
  gender: Gender
}

schema {
  query: Query
  mutation: Mutation
  subscription: Subscription
}
```

### 1-4. Try Mutation createBook to add some data at the 'Queries' page

```
mutation create{
  createBook(input:{title:"水许", author:"师奶庵", gender:Male}) {
    title
    author
    gender
  }
}
```


```
mutation create{
  createBook(input:{title:"嘻游记", author:"无承恩", gender:Male}) {
    title
    author
    gender
  }
}
```

```
mutation create{
  createBook(input:{title:"原始物語", author:"姿势部", gender:Female}) {
    title
    author
    gender
  }
}
```

**Check DynamoDB**
| title (S) | gender (S) | author (S) |
| ----------|----------- |------------|
| 水许       | Male       | 师奶庵      |
| 嘻游记     | Male       | 无承恩      |
| 原始物語   | Female     | 姿势部      |

### 1-5. Try Query getBook at the 'Queries' page

```
query getBook{
  getBook(title:"水许") {
    title
    author
    gender
  }
}
```

```
{
  "data": {
    "getBook": {
      "title": "水许",
      "author": "师奶庵",
      "gender": "Male"
    }
  }
}
```

### 1-6. Add Resolver for Query getAllBooks and test
* Data source name: BookTable
* Request mapping template
```
{
    "version": "2017-02-28",
    "operation": "Scan"
}
```
* Response mapping template
```
$utils.toJson($context.result.items)
```

**Try Query getAllBooks at the 'Queries' page**

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
{
  "data": {
    "getAllBooks": [
      {
        "title": "嘻游记",
        "author": "无承恩",
        "gender": "Male"
      },
      {
        "title": "水许",
        "author": "师奶庵",
        "gender": "Male"
      }
    ]
  }
}
```

## 2. Manually Setup Vue application

### 2-1. Check Node version
**Make sure you have Node v9+**

```
$ node -v
```

### 2-2. Check vue-cli & awsmobile-cli version
**Make sure you have vue-cli 3+**

```
$ npm install -g @vue/cli@3.12.1
$ vue --version
```

**Make sure you have awsmobile-cli 1.1.x**
```
$ npm install -g awsmobile-cli
$ awsmobile --version
```

### 2-3. Create a vue project
```
$ vue create vue-appsync-study-example
Vue CLI v3.12.1

? Please pick a preset: 
  default (babel, eslint) 
❯ Manually select features 

? Please pick a preset: Manually select features
? Check the features needed for your project: 
 ◉ Babel
 ◯ TypeScript
 ◯ Progressive Web App (PWA) Support
❯◉ Router
 ◯ Vuex
 ◯ CSS Pre-processors
 ◯ Linter / Formatter
 ◯ Unit Testing
 ◯ E2E Testing

? Use history mode for router? (Requires proper server setup for index fallback in production) Yes
? Where do you prefer placing config for Babel, PostCSS, ESLint, etc.? (Use arrow keys)
❯ In dedicated config files 
  In package.json 


```

### 2-4. Apply the AppSync plugin
**Navigate to the newly created project folder and add the cli plugin:**

```
$ cd vue-appsync-study-example
$ vue add appsync

? Add an AppSync Example page? Yes
? What is the datasource type? AMAZON_DYNAMODB
? What is the authentication type? API_KEY
? Deploy the AWS AppSync and AWS Mobile Hub Backends? No
```

### 2-5. Modify aws-exports.js
**Edit or create src/aws-exports.js.**
**All the AppSync info can be retrieved at AWS AppSync management console.**
```
const awsmobile = {
    'aws_appsync_graphqlEndpoint': 'https://<your_appsync_endpoint>.appsync-api.<your_region>.amazonaws.com/graphql',
    'aws_appsync_region': '<your_region>',
    'aws_appsync_authenticationType': 'API_KEY',
    'aws_appsync_apiKey': '<your_api_key>',
}

export default awsmobile;
```

### 2-6. Start your app
```
$ npm run serve
```

### 2-7. Access http://localhost:8080 and play with the AppSyncExample
![GraphQL Client App](vue-appsync-study/app.png)
**Check DynamoDB 'BookTable' for mutation results**

### 2-8. Stop node Node processes
