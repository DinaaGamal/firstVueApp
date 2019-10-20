<template>
  <el-card class="box-card">
    <div class="clearfix" v-bind:class="{'is-completed':todo.completed}">
      <el-checkbox v-model="checked" v-on:change="completeTodo" />
      <span class="text item">{{todo.title}}</span>
      <el-button
        @click="$emit('del-todo',todo.id)"
        class="del"
        type="danger"
        icon="el-icon-delete"
        circle
        style="float: right; padding: 3px"
      ></el-button>
    </div>
  </el-card>
</template>
<script>
// import { Button } from "element-ui";
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    completeTodo() {
      this.todo.completed = !this.todo.completed;
    }
  },
  data() {
    return {
      checked: false
    };
  }
};
</script>
<style scoped>
.todo-item {
  color: rgb(88, 88, 88);
}
.is-completed {
  text-decoration: line-through;
}
.del {
  /* background-color: rgb(34, 34, 34); */
  color: white;
  width: 30px;
  height: 30px;
}
.text {
  font-size: 17px;
  word-wrap: break-word;
}

.clearfix:before,
.clearfix:after {
  display: table;
  content: "";
}
.clearfix:after {
  clear: both;
}

.box-card {
  width: 480px;
  justify-items: center;
  margin-left: 35%;
  margin-top: 20px;
}
</style>