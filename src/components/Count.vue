<template>
  <div class="count">
    <button @click="increment">Count is: {{state.count}}, double is: {{state.double}}</button>
  </div>
</template>

<script>
import { reactive, computed } from "@vue/composition-api";

export default {
  name: "Count",

  setup() {
    const state = reactive({
      count: 0,
      double: computed(() => state.count * 2)
    });

    const increment = () => state.count++;

    return {
      state,
      increment
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
