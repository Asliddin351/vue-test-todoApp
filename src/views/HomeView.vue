<template>
  <h1>Todo App</h1>
  <todo-app/>
</template>
<script lang="ts">
import { defineComponent } from 'vue'
import TodoApp from '../components/TodoApp.vue'

export default defineComponent({
  name: "home-view",
  components: { TodoApp }
})

</script>
<style lang="css">
h1 {
  text-align: center;
}
</style>
