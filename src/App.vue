<template>
  <div id="app">
    <Day />
  </div>
</template>

<script>
import Day from "./components/Day";

export default {
  components: {
    Day
  }
};
</script>

<style>
#app {
  font-family: Roboto, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
