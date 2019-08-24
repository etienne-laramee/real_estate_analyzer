<template>
  <div>
    <div v-bind:key="entry.Id" v-for="entry in entries">
      <TodoItem v-bind:entry="entry" v-on:del-todo="$emit('del-todo', entry.id)" />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  name: "Todos",
  components: {
    TodoItem
  },
  props: ["entries"]
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
