<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <TodoHeader @addTodo="addTodo"></TodoHeader>
      <TodoList :todos="todos"></TodoList>
      <TodoFooter
        :todos="todos"
        @checkAllTodo="checkAllTodo"
        @clearAllTodo="clearAllTodo"
      ></TodoFooter>
    </div>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
  name: "App",
  components: {
    TodoHeader,
    TodoList,
    TodoFooter,
  },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem("todos")) || [],
    };
  },
  methods: {
    addTodo(todoObj) {
      this.todos.unshift(todoObj);
    },
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) todo.done = !todo.done;
      });
    },
    handleRemove(id) {
      this.todos = this.todos.filter((todo) => {
        return todo.id !== id;
      });
    },
    checkAllTodo(done) {
      this.todos.forEach((todo) => {
        todo.done = done;
      });
    },
    clearAllTodo() {
      this.todos = this.todos.filter((todo) => {
        return !todo.done;
      });
    },
    updateTodo(id, title) {
      this.todos.forEach((todo) => {
        if (todo.id == id) {
          todo.title = title;
        }
      });
    },
  },
  watch: {
    todos: {
      deep: true,
      handler(newVal) {
        localStorage.setItem("todos", JSON.stringify(newVal));
      },
    },
  },
  mounted() {
    this.$bus.$on("checkTodo", this.checkTodo);
    this.$bus.$on("handleRemove", this.handleRemove);
    this.$bus.$on("updateTodo", this.updateTodo);
  },
  beforeDestroy() {
    this.$bus.$off("checkTodo");
    this.$bus.$off("handleRemove");
    this.$bus.$off("updateTodo");
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
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  background-repeat: 5px;
}
.btn-danger {
  background-color: red;
  color: white;
  border: none;
}
.btn-edit {
  background-color: skyblue;
  color: white;
  border: none;
}
</style>
