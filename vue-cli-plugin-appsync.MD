# Part V. Create frontend and backend together

**Create Vue.js Application & Appsync with [vue-cli-plugin-appsync](https://github.com/komushi/vue-cli-plugin-appsync) and [AWS Mobile CLI](https://aws.github.io/aws-amplify/media/cli_guide)**

**:rocket: This is how I created a Vue Application with AppSync in one minute!**

## 1. Check Node version
:warning: Make sure you have Node v9.x.x:

```
node -v
```

## 2. Check vue-cli version
:warning: Make sure you have vue-cli 3.x.x:

```
vue --version
```

## 3. Check AWS Mobile CLI version:
:warning: Make sure you have awsmobile-cli 1.1.x:

```
awsmobile -V
```

### 4. Configure AWS Mobile CLI:
**Choose your region**

```
$awsmobile configure aws

configure aws
? accessKeyId:  <accessKeyId>
? secretAccessKey:  <secretAccessKey>
? region:  ap-northeast-1
```


## 5. Setup Vue application
### 5-1. Create a vue project
**Use Babel, Router, Linter with default settings**
```
vue create my-new-app

Vue CLI v3.0.0-beta.15
? Please pick a preset: Manually select features
? Check the features needed for your project: 
 ◉ Babel
 ◯ TypeScript
 ◯ Progressive Web App (PWA) Support
❯◉ Router
 ◯ Vuex
 ◯ CSS Pre-processors
 ◉ Linter / Formatter
 ◯ Unit Testing
 ◯ E2E Testing
```

### 5-2. Apply the AppSync plugin
```
cd my-vue-appsync-app
vue add appsync

? Add an AppSync Example page? Yes
? What is the authentication type? AMAZON_COGNITO_USER_POOLS
? Deploy the AWS AppSync and AWS Mobile Hub Backends? Yes
```

### 5-3. Check the AppSync settings example at awsmobilejs/backend/appsync
```
./awsmobilejs/
└── backend
    ├── appsync
    │   ├── apiKeys.json
    │   ├── dataSources.json
    │   ├── graphqlApi.json
    │   ├── resolver-mappings
    │   │   ├── Mutation.createBook.request
    │   │   ├── Mutation.createBook.response
    │   │   ├── Mutation.deleteBook.request
    │   │   ├── Mutation.deleteBook.response
    │   │   ├── Mutation.updateBook.request
    │   │   ├── Mutation.updateBook.response
    │   │   ├── Query.getAllBooks.request
    │   │   ├── Query.getAllBooks.response
    │   │   ├── Query.getBook.request
    │   │   ├── Query.getBook.response
    │   │   ├── Query.getBooksByGender.request
    │   │   ├── Query.getBooksByGender.response
    │   │   ├── Query.listBooks.request
    │   │   └── Query.listBooks.response
    │   ├── resolvers.json
    │   └── schema.graphql
    └── mobile-hub-project.yml
```

### 5-4. Start your app

```
npm run serve
```

*Or*

```
awsmobile run
```

## 6. Access http://localhost:8080/ and play with the Vue application with the support of AWS AppSync API

## 7. Stop the Node process
