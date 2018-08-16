# Part III. Vue.js Application connecting to Apollo GraphQL

**Use vue-cli-plugin-apollo to start a Vue.js Application with Apollo GraphQL backend**

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

## 3. Create this Vue.js application by vue-cli 3.x.x and vue-cli-plugin-apollo
### 3-1. Create project
```
$ vue create vue-apollo-study
```

### 3-2. Add apollo plugin by vue-cli-plugin-apollo
```
$ cd vue-apollo-study
$ vue add apollo

? Add example code Yes
? Add a GraphQL API Server? No
```

### 3-3. Edit App.vue to inclued the ApolloExample.vue - below is the expected code
```
<template>
  <div id="app">
    <img src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <apollo-example></apollo-example>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ApolloExample from './components/ApolloExample.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    ApolloExample
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

### 3-4. Edit main.js to include vue-apollo provider - below is the expected code
```
import Vue from 'vue'
import App from './App.vue'
import { createProvider } from './vue-apollo'

Vue.config.productionTip = false

new Vue({
  provide: createProvider().provide(),
  render: h => h(App)
}).$mount('#app')

```

## 4. Play with the application
### 4-1. Start the Apollo GraphQL backend created at [Part II](/apollo-express-study.MD#5-3-start-the-graphql-api-server)

### 4-2. Start the Vue.js application
```
$ npm run serve
```

### 4-3. Access http://localhost:8080/ and play with ApolloExample
![GraphQL Client App](https://raw.githubusercontent.com/komushi/vue-apollo-study/master/image/image2.png)

### 4-4. Stop the Client and Server Node processes

# Reference: 
* [vue-apollo-study](https://github.com/komushi/vue-apollo-study)
