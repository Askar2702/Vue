<template>
  <div id="app"><TodoAppVue></TodoAppVue></div>
</template>
<script>
import TodoAppVue from "./components/TodoApp.vue";

export default {
  name: "app",
  components: {
    TodoAppVue,
  },
};
</script>
