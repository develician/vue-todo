<template>
  <div class="app">
    <todo-app />
  </div>
</template>

<script>
import TodoApp from "./components/TodoApp.vue";

export default {
  name: "app",
  components: {
    TodoApp
  }
};
</script>

<style>
@import "~open-color/open-color.css";
body {
  margin: 0;
  box-sizing: border-box;
  background: var(--oc-indigo-1);
}

.app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: calc(100vh);
}
</style>
