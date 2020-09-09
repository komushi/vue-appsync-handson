# Part III. Vue.js Application connecting to Apollo GraphQL

**Use vue-cli-plugin-apollo to start a Vue.js Application with Apollo GraphQL backend**

## 1. Check Node version
**Make sure you have Node v9+**

```
$ node -v
```

## 2. Check vue-cli version
**Make sure you have vue-cli 3+ or 4+**

```
$ npm install -g @vue/cli
$ vue --version
```

## 3. Create this Vue.js application by vue-cli 3.x.x and vue-cli-plugin-apollo
### 3-1. Create project
```
$ vue create vue-apollo-study
Vue CLI v4.5.4
? Please pick a preset: 
❯ Default ([Vue 2] babel, eslint) 
  Default (Vue 3 Preview) ([Vue 3] babel, eslint) 
  Manually select features 

? Please pick a preset: Default ([Vue 2] babel, eslint)
? Pick the package manager to use when installing dependencies: 
  Use PNPM 
❯ Use NPM 
```

### 3-2. Add apollo plugin by vue-cli-plugin-apollo
```
$ cd vue-apollo-study
$ vue add apollo

? Add example code Yes
? Add a GraphQL API Server? No
? Configure Apollo Engine? No
```

## 4. Play with the application
### 4-1. Start the Apollo GraphQL backend created at [Part II](apollo-express-study/apollo-express-study.MD#5-3-start-the-graphql-api-server)

### 4-2. Start the Vue.js application
```
$ npm run serve
```

### 4-3. Access http://localhost:8080/ and play with ApolloExample
![GraphQL Client App](https://raw.githubusercontent.com/komushi/vue-apollo-study/master/image/image2.png)

### 4-4. Stop the Client and Server Node processes
