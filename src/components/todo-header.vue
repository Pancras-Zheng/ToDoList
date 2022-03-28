<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="addTodo"/>
  </div>
</template>

<script>
import {nanoid} from "nanoid";

export default {
  name: "todo-header",
  //接收父组件传入的数据（函数类型）
  props: ['receive'],
  data() {
    return {
      title: ''
    }
  },
  methods: {
    //增加待办项
    addTodo() {
      // console.log(e.target.value)
      //校验输入内容
      if (!this.title.trim()) return alert('输入内容不可为空')
      //将用户输入包装为对象
      const todoObj = {id: nanoid(), title: this.title, done: false};
      //通知app:添加一个 todoObj 对象
      this.receive(todoObj)
      //清空输入框
      this.title = ''
    },
  }
}
</script>

<style scoped>
/*header*/
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
}
</style>