<template>
  <div id="app">
    <CryptoApp />
  </div>
</template>

<script>
import CryptoApp from "./components/CryptoApp.vue";

export default {
  components: {
    CryptoApp,
  },
};
</script>

<style>
body {
  background: #1a1a1c !important;
}
#app {
  font-family: "Quicksand", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #fff;
  margin: 40px 0 30px 0;
}
</style>
