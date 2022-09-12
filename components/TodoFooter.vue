<template>
  <div class="todo-footer" v-show="total">
    <label>
      <!-- <input type="checkbox" :checked="isAll" @change="checkAll" /> -->
      <input type="checkbox" v-model="isAll" />
    </label>
    <span
      ><span>已完成{{ doneTolal }}</span> / 全部{{ total }}</span
    >
    <button class="btn" @click="removeComplete">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "TodoFooter",
  props: ["todos"],
  computed: {
    total() {
      return this.todos.length;
    },
    // pre参数为初始值，当遍历第二次的时候它的值是遍历第一次时的返回值，current为当前遍历的对象
    doneTolal() {
      return this.todos.reduce((pre, current) => {
        return pre + (current.done ? 1 : 0);
      }, 0);
    },
    // isAll() {
    //   return this.doneTolal === this.total && this.total > 0;
    // },
    isAll: {
      get() {
        return this.doneTolal === this.total && this.total > 0;
      },
      set(val) {
        this.$emit("checkAllTodo", val);
      },
    },
  },
  methods: {
    // checkAll(e) {
    //   this.$emit("checkAllTodo", e.target.checked);
    // },
    removeComplete() {
      this.$emit("clearAllTodo");
    },
  },
};
</script>

<style>
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}
.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}
.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}
.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>
