<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>Welcome to Vuex Hello World App</h1>
    <Form />
    <Display />
  </div>
</template>

<script>
import Form from "./components/Form";
import Display from "./components/Display";

export default {
  name: "App",
  components: {
    Form,
    Display,
  },
};
</script>

