<template>
  <div style="margin-top: 20px;">
    <div v-if="api_status === 'FETCHING'">Fetching</div>
    <div v-else-if="api_status === 'FETCHING_ERROR'">Error</div>
    <div v-else-if="api_status === 'FETCHING_SUCCESS'">
      <img :src="dogImage" style="display: block; max-width: 500px; height: auto; margin: 0 auto;" />
    </div>
    <div v-else>Oops, no dog found</div>
    <button style="margin-top: 20px;" @click.prevent="fetchDog">Fetch dog</button>
  </div>
</template>

<script>
import { reactive, computed, toRefs } from "@vue/composition-api";

const useApi = (url, options = {}) => {
  const state = reactive({
    data: null,
    api_status: ""
  });

  const initFetch = async () => {
    try {
      state.api_status = "FETCHING";
      const response = await fetch(url);
      const data = await response.json();
      state.data = data.message;
      state.api_status = "FETCHING_SUCCESS";
    } catch (error) {
      state.api_status = "FETCHING_ERROR";
    }
  };

  if (options.hasOwnProperty("fetchImmediately") && options.fetchImmediately) {
    initFetch();
  }

  return {
    ...toRefs(state),
    initFetch
  };
};

export default {
  setup() {
    const { data, api_status, initFetch } = useApi(
      "https://dog.ceo/api/breeds/image/random",
      {
        fetchImmediately: true
      }
    );

    return {
      dogImage: data,
      api_status,
      fetchDog: initFetch
    };
  }
};
</script>

<style lang="scss" scoped>
</style>