<template>
  <SuperButton />
</template>

<script>
import SuperButton from "@/components/SuperButton.vue";

export default {
  name: "App",
  components: {
    SuperButton,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
