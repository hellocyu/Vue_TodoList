<template>
  <ul class="todo-main">
    <TodoItem v-for="todoObj in todos" :key="todoObj.id" :todo="todoObj">
    </TodoItem>
  </ul>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  name: "TodoList",
  components: {
    TodoItem,
  },
  props: ["todos"],
};
</script>

<style scoped>
.todo-main {
  margin-left: 8px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}
.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>
