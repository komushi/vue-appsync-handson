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

## 4. Manually Setup Vue application
### 4-1. Create a vue project
```
vue create my-vue-appsync-app
```

### 4-2. Apply the AppSync plugin
```
cd my-vue-appsync-app
vue add appsync
```

### 4-3. Check the AppSync settings example at awsmobilejs/backend/appsync
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

### 4-4. Create the backend
**Check the MobileHub Backend, the AppSync Backend & the DynamoDB Table after**
```
awsmobile init --yes
```

### 4-5. Start your app

```
npm run serve
```

*Or*

```
awsmobile run
```

## 5. Access http://localhost:8080/ and play with the Vue application with the support of AWS AppSync API

## 6. Stop the Node process

## 7. Challenges

### 7-1: Create UpdateBook and Subscription for OnUpdateBook

### 7-2: Update my-vue-appsync-study/src/components/AppSyncExample.vue to enable 'Book info edit'

# Reference: 
* [vue-appsync-study](https://github.com/komushi/vue-appsync-study#option-i-streamlined-approach-by-using-vue-cli-plugin-appsync-and-aws-mobile-cli)