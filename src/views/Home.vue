<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todo v-bind:todos="todos" v-on:del-todo="deleteTodo" />
    <!-- <div v-for="customer in customers" v-bind:key="customer._id">
      <Customers v-bind:customer="customer" />
    </div> -->
  </div>
</template>

<script>
import axios from "axios";

import Todo from "../components/Todo";
import AddTodo from "../components/AddTodo";
import Customers from '../components/Customers'

export default {
  name: "home",
  components: {
    // Customers
    Todo,
    AddTodo
  },
  data() {
    return {
      todos: [
        
      ],
      customers: []
    };
  },
  methods: {
    deleteTodo(id) {
      // this.todos = this.todos.filter(td => td.id !== id);
      axios.delete(`https://jsonplaceholder.typecode.com/todos/${id}`)
      .then(res => this.todos = this.todos.filter(td => td.id !== id))
      .catch(err => console.log(err))
    },
    addTodo(todo) {

      const { title, completed } = todo
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title, completed
      })
      .then(res => this.todos = [...this.todos, res.data])
      .catch(err => console.log(err))
      // this.todos = [...this.todos, todo];
    }
  },
  created() {
    axios
      .get("http://jsonplaceholder.typicode.com/todos?_limit=7")
      .then(res => {
        console.log(res)
        this.todos = res.data
      })
      .catch(err => {});
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Roboto", sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #455;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
