<template>
  <div class="main_app">
    <Calculator />
    <div class="tech-stack">
      <ion-icon name="logo-vue"></ion-icon>
      <ion-icon name="logo-html5"></ion-icon>
      <ion-icon name="logo-nodejs"></ion-icon>
    </div>
  </div>
</template>

<script>
import Calculator from "./components/Calculator.vue";

export default {
  name: "App",
  components: {
    Calculator,
  },
};
</script>

<style>
body {
  background: #44a08d; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #093637,
    #44a08d
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #093637,
    #44a08d
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 150px;
}
</style>
