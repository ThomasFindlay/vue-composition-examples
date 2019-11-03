<template>
  <div id="app">
    <Count />
    <Dog />
  </div>
</template>

<script>
import Count from "@/components/Count";
import Dog from "@/components/Dog";
export default {
  name: "app",
  components: { Count, Dog }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
