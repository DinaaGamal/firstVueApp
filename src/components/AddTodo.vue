<template>
  <div>
    <form @submit="addTodo">
      <input v-model="title" type="text" placeholder="Enter Todo ..." />
      <el-button @click="addTodo" type="danger" class="btn">Add New Todo</el-button>
    </form>
  </div>
</template>
<script>
import uuid from "uuid/v4";
export default {
  name: "AddTodo",
  date() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        id: uuid(),
        title: this.title,
        completed: false
      };
      this.$emit("add-todo", newTodo);
      this.title = "";
    }
  }
};
</script>
<style scoped>
form {
  display: flex;
}
input[type="text"] {
  flex: 10;
  padding: 5px;
}
input[type="submit"] {
  flex: 2;
}
</style>