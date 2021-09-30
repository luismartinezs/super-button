<template>
  <div class="wrapper">
    <SuperButton />
  </div>
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
html,
body {
  width: 100%;
  height: 100%;
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  width: 100%;
  height: 100%;
  margin: 0;
  background: hsl(200deg, 5%, 50%);
}

.wrapper {
  padding-top: 40px;
}
</style>
