
## Purpose of this tutorial

Learn the official Vue3 tutorial using vue-cli v4.5.

Note: In this tutorial, the display looks like a Unix terminal, and you can actually see it on these operating systems, but you can actually do the same with Windows Terminal and PowerShell Window.

*The original article of this tutorial is this URL*

https://v3.vuejs.org/guide/introduction.html

## 1. Until the first Vue3 app is displayed in the browser


### Install vue-cli

The official documentation does not recommend using vue-cli for beginners with such a statement.

> We **do not** recommend that beginners start with vue-cli, especially if you are not yet familiar with Node.js-based build tools.

However, it is difficult to understand the work contents in actual development without utilizing such command line tools.

```bash
$ npm install -g @vue/cli
+ @vue/cli@4.5.12
$ vue --version
@vue/cli 4.5.12
$
```

### Create a new project

A set of project files for a single-page web app using Vue3 is created concisely on the command line.

```
$ vue create hellow-world
Vue CLI v4.5.12
? Please pick a preset: (Use arrow keys)
  Default ([Vue 2] babel, eslint)
> Default (Vue 3 Preview) ([Vue 3] babel, eslint)
  Manually select features
```

to select [Vue 3]

The generated project directory is 'hello-world'.

However, the node_modules directory is omitted, so when checking this directory by itself, execute'$ npm install'.


```
$ cd hello world
$ npm run serve
 DONE  Compiled successfully in 5879ms    17:10:56


  App running at:
  - Local:   http://localhost:8080/
  - Network: http://192.168.10.110:8080/

  Note that the development build is not optimized.
  To create a production build, run yarn build.
```

Access the URL displayed in the terminal with a browser.

You can see the page. [hello-world](result-hello-world.png)


## 2. Declarative Rendering

At the core of Vue.js is a system that enables us to declaratively render data to the DOM using straightforward template syntax:

### Initialize the counter

Modify the 'hello-world' project to see how your web application behaves in front of you.

Edit *src/components/HelloWorld.vue*

```webpack
<template>
  <div id="counter" class="demo">
    Counter: {{ msg }}
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.demo {
  font-family: sans-serif;
  border: 1px solid #eee;
  border-radius: 2px;
  padding: 20px 30px;
  margin-top: 1em;
  margin-bottom: 40px;
  user-select: none;
  overflow-x: auto;
}
</style>
```

You can see the page. [counter-text](result-counter-text.png)

This looks pretty similar to rendering a string template, but Vue has done a lot of work under the hood. The data and the DOM are now linked, and everything is now reactive.


The string **Welcome to Your Vue.js App** is initialized from the following in *src/App.vue* .

> <Hello World msg = "Welcome to Your Vue.js App"/>

Let's change the counter displayed on the screen to a number and change it every second.

### Turn the counter

Edit *src/components/HelloWorld.vue*

```webpack
...
<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      msg: 0
    }
  },
  mounted() {
    setInterval(() => {
      this.msg++
    }, 1000)
  }
}
</script>
...
```

You can see the page. [hello-world2](result-hello-world2.png)

The result project directory is 'hello-world2'.

## 3. Update tag attributes

With Vue3, you can directly change the attribute of the tag specified in the JavaScript calculation result.

```webpack
<template>
  <div id="bind-attribute" class="demo">
    <span v-bind:title="msg">
      Hover your mouse over me for a few seconds to see my dynamically bound
      title!
    </span>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      msg: 'You loaded this page on ' + new Date().toLocaleString()
    }
  }
}
</script>
...
```

You can see the page. [hello-world2](result-hello-world3.png)

Note: In the Google Chrome browser, pop-up text is displayed when hovering the mouse. Other web browsers may give different results.

The result project directory is 'hello-world3'.

Here we're encountering something new. The v-bind attribute you're seeing is called a directive. Directives are prefixed with v- to indicate that they are special attributes provided by Vue, and as you may have guessed, they apply special reactive behavior to the rendered DOM. Here we are basically saying "keep this element's title attribute up-to-date with the message property on the current active instance."

## 4. Handling User Input

To let users interact with your app, we can use the v-on directive to attach event listeners that invoke methods on our instances:

```webpack
<template>
  <div id="event-handling">
    <p>{{ msg }}</p>
    <button v-on:click="reverseMessage">Reverse Message</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      msg: 'Hello Vue.js!'
    }
  },
  methods: {
    reverseMessage() {
      this.msg = this.msg
        .split('')
        .reverse()
        .join('')
    }
  }
}
</script>
...
```

You can see the page. [hello-world2](result-hello-world4.png)

The result project directory is 'hello-world4'.

## 5. Add a new component

Why does this tutorial do the same thing on the official Vue.js page in a different way in the first place?

It is because it benefits from webpack.

When you create a Vue3 project with vue-cli, the source code is divided into **App.vue** and **HelloWorld.vue** from the beginning. Of course, this can be rewritten as well as added.

Edit a new file, **src/components/InputMessage.vue**

```webpack
<template>
  <div id="two-way-binding">
    <p>{{ message }}</p>
    <input v-model="message" />
  </div>
</template>

<script>
export default {
  name: 'TwoWayBinding',
  data() {
    return {
      message: 'Hello Vue!'
    }
  }
}
</script>
```

Edit **src/App.vue**

```webpack
<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <InputMessage message="Hello Vue!"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import InputMessage from './components/InputMessage.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    InputMessage
  }
}
</script>
...
```

You can see the page. [hello-world5](result-hello-world5.png)

The result project directory is 'hello-world5'.
