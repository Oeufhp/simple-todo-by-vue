<template>
  <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
    <input type="checkbox" v-on:change="markComplete" />
    <p>{{ todo.title }}</p>
    <button class="del" @click="$emit('del-todo', todo.id)">X</button>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    },
  }
};
</script>

<style scoped>
  .todo-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
    display: flex;
    justify-content: space-between;
  }
  .is-complete {
    text-decoration: line-through;
  }
  .del {
    background: #ff0000;
    color: #fff;
    padding: 5px 9px;
    border-radius: 50%;
    border: none;
    outline: none;
  }
</style>
