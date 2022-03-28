<template>
  <ul class="todo-main" >
    <todo-item v-for="(todoObj) in todos" :key="todoObj.id" :todo="todoObj" :checkTodo="checkTodo"
               :deleteTodo="deleteTodo"></todo-item>
  </ul>
</template>

<script>
import todoItem from "@/components/todo-item";

export default {
  name: "todo-list",
  //注册子组件  todoItem
  components: {
    todoItem
  },
  //接收app传入的data
  props: ['todos', 'checkTodo', 'deleteTodo']
}
</script>

<style scoped>
/*main*/
.todo-main {
  margin-left: 0px;
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