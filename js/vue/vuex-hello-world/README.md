# Vuex Hello World

* [Full tutorial](https://flaviocopes.com/vuex/)
* [Online demo on codesandbox](https://codesandbox.io/s/zq7k7nkzkm)

Vuex is the official state management library for Vue.js. Its job is to share data across the components of your application.

Components in Vue.js out of the box can communicate using:

* **props**, to pass state down to child components from a parent.
* **events**, to change the state of a parent component from a child, or using the root component as an event bus.

## Project setup
```
npm install vuex
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

## Project tutorial

The project will consists of 2 sibling components, one with an input field, and one that prints that input field content. When the input field is changed, the content is printed in that second component. 

The first step is to create the store `src/store/index.js`.

We create two components [Display.vue](src/components/Display.vue) and [Form.vue](src/components/Form.vue).

Next they need to be added to [App.vue](App.vue), with a reference in the template and another one in the script.

```vue
<template>
  <div id="app">
    <Form/>
    <Display/>
  </div>
</template>

<script>
import Form from './components/Form'
import Display from './components/Display'

export default {
  name: 'App',
  components: {
    Form,
    Display
  }
}
</script>

```

In [index.js](src/store/index.js), we add the property `state: { flavor: '' }` which is the input form name.

To manipulate the state we use mutations. One mutation which will be used inside the Form component to notify the store that the state should change.

```js
export const store = new Vuex.Store({
  state: {
    flavor: ''
  },
  mutations: {
    change(state, flavor) {
      state.flavor = flavor
    }
  }
})

```

Then we need to add a way to look at the state. We do so using getters. We set up a getter for the flavor property. Notice how getters is an object. flavor is a property of this object, which accepts the state as the parameter, and returns the flavor property of the state.

```js
export const store = new Vuex.Store({
  state: {
    flavor: ''
  },
  mutations: {
    change(state, flavor) {
      state.flavor = flavor
    }
  },
  getters: {
    flavor: state => state.flavor
  }
})
```

Let’s create a method that is invoked when the input content changes. We use `@input` rather than `@change` because the latter is only triggered when the focus is moved away from the input box, while `@input` is called on every keypress.

In [Form.vue](src/components/Form.vue) add:

```vue
<template>
  <div>
    <label for="flavor">Favorite ice cream flavor?</label>
    <input @input="changed" name="flavor">
  </div>
</template>

<script>
export default {
  methods: {
    changed: function(event) {
      this.$store.commit('change', event.target.value)
    }
  }
}
</script>
```

The `commit()` method accepts a mutation name (we used change in the Vuex store) and a payload, which will be passed to the mutation as the second parameter of its callback function.

Now we need to reference the getter of this value in the [Display.vue](src/components/Display.vue) template, by using `$store.getters.flavor`. `this` can be removed because we’re in the template, and this is implicit.

```vue
<template>
  <div>
    <p>You chose {{ $store.getters.flavor }}</p>
  </div>
</template>
```

