<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
    <Footer />
  </div>
</template>

<script>
import Todos from "./components/Todos";
import Header from "./components/layout/Header";
import Footer from "./components/layout/Footer";
import AddTodo from "./components/AddTodo";
import Axios from "axios";

export default {
  name: "app",
  components: {
    Header,
    Todos,
    AddTodo,
    Footer
  },

  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      Axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`).then(
        () => (this.todos = this.todos.filter(todo => todo.id !== id))
      );
    },
    addTodo(newTodo) {
      const { title, completed, id } = newTodo;
      Axios.post("https://jsonplaceholder.typicode.com/todos", {
        id,
        title,
        completed
      }).then(res => {
        console.log(res);
        this.todos = [...this.todos, res.data];
      });
      // .catch(err => console.log(err));
    }
  },

  // like component did mount func here where we fetch our data//
  created() {
    //fetchdata

    Axios.get("https://jsonplaceholder.typicode.com/todos?_limit=7").then(
      res => {
        console.log(res);
        this.todos = res.data;
      }
    );

    // .catch(err => console.log(err));
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
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;

  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn-hover {
  background: #666;
}
</style>
