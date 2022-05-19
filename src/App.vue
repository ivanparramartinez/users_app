<template>
  <div id="app">
    <UsersApp />
  </div>
</template>

<script>
import UsersApp from "@/components/UsersApp.vue";

export default {
  name: "App",
  components: {
    UsersApp,
  },
};
</script>

<style>
#app {
  font-family: "Avenir Next", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}

* {
  box-sizing: border-box;
  font-size: 12px;
}

@media screen and (min-width: 768px) {
  * {
    font-size: 14px;
  }
}

@media screen and (min-width: 1024px) {
  * {
    font-size: 16px;
  }
}
</style>
