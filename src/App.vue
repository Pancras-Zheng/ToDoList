<template>
  <div id="root">
    <div class="todo-container">
      <img alt="Vue logo" src="./assets/logo.png">
      <!-- 向header传入参数：receive接收函数-->
      <div class="todo-wrap">
        <todo-header :receive="receive"/>
        <todo-list :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"></todo-list>
        <todo-footer :todos="todos" :checkAllTodo="checkAllTodo" :deleteAllTodo="deleteAllTodo"></todo-footer>
      </div>
    </div>
  </div>
</template>

<script>
import todoHeader from './components/todo-header'
import todoFooter from './components/todo-footer'
import todoList from "./components/todo-list";

export default {
  name: 'App',
  data() {
    return {
      todos: JSON.parse(localStorage.getItem('todos')) || []
    }
  },
  components: {
    todoHeader,
    todoFooter,
    todoList,
  },
  methods: {
    //接收header传回的 todoObj 对象
    receive(todoObj) {
      this.todos.unshift(todoObj);
    },
    //勾选or取消勾选todo
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) {
          todo.done = !todo.done
        }
      })
    },
    //删除一个todo
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => {
        return todo.id !== id
      })
    },
    //全选/全不选操作
    checkAllTodo(done) {
      this.todos.forEach((todo) => {
        todo.done = done
      })
    },
    // 清楚所有
    deleteAllTodo() {
      this.todos = this.todos.filter((todo) => {
        return !todo.done
      })
    }
  },
  watch: {
    todos: {
      deep: true,
      handler(value) {
        localStorage.setItem('todos', JSON.stringify(value))
      }
    }
  }
}
</script>

<style>

body {
  background: #fff;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}

.todo-container .todo-wrap {

  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

img {
  width: inherit;
}
</style>
