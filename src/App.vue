<template>
  <div id="app">
    <tags />
  </div>
</template>

<script>
import Tags from "./components/tags.vue";

export default {
  name: "App",
  components: {
    Tags,
  },
};
</script>


<style>
** {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
</style>
