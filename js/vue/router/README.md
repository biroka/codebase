# Router

* [Full tutorial](https://flaviocopes.com/vue-router/)
* [Online demo on codesandbox](https://codesandbox.io/s/zq7k7nkzkm)


In a JavaScript web application, a router is the part that syncs the currently displayed view with
the browser address bar content. You need a router when you need to sync URLs to views in your app.

## Project setup
```
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

In the template I use a nav tag that has 3 router-link components, which have a label (Home/Login/About) and a URL assigned through the to attribute. The router-view component is where the Vue Router will put the content that matches the current URL. 

A router-link component renders an a tag by default (you can change that). Every time the route changes, either by clicking a link or by changing the URL, a router-link-active class is added to the element that refers to the active route, allowing you to style it.

In [App.vue](src/App.vue), we can add:

```vue
<template>
  <div id="app">
    <nav>
      <router-link to="/">Home</router-link>
      <router-link to="/about">About</router-link>
    </nav>
    <router-view></router-view>
  </div>
</template>
```

The components can be defined in [src/router/index.js](src/router/index.js).

### Dynamic routing

A very common need is to handle dynamic routes, like having all posts under /post/, each with the slug name:

* /post/first
* /post/another-post
* /post/hello-world

This can be handled:

```vue
const router = new VueRouter({
  routes: [
    { path: '/', component: Home },
    { path: '/post/:post_slug', component: Post },
    { path: '/about', component: About }
  ]
})
```

Vue to be more efficient instead of destroying the current route component and re-instantiating it, it reuses the current instance. When this happens, Vue calls the beforeRouteUpdate life cycle event. There you can perform any operation you need:

In the Post view:

```vue
beforeRouteUpdate(to, from, next) {
    console.log(`Updating slug from ${from} to ${to}`)
    next() //make sure you always call next()
}
```