<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" width="25%" />
    <DropdownSearch msg="Dropdown with Search" />
  </div>
</template>

<script>
import DropdownSearch from "./components/DropdownSearch";

export default {
  name: "App",
  components: {
    DropdownSearch,
  },
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
