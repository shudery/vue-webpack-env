<template>
  <div id="app">
    <my-demo></my-demo>
  </div>
</template>

<script>
import myDemo from "./components/demo";

export default {
  data: () => {
    return {
      data: "daguo"
    };
  },
  name: "app",
  components: {
    "my-demo": myDemo
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
