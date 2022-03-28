<template>
  <div class="todo-footer" v-show="total">
    <label>
<!--      <input type="checkbox" :checked="isAll" @change="checkAll"/>-->
      <input type="checkbox" v-model="isAll"/>
    </label>
    <span>
          <span>已完成{{ doneTotal }}</span> / 全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "todo-footer",
  props: ['todos', 'checkAllTodo','deleteAllTodo'],
  computed: {
    total() {
      return this.todos.length
    },
    doneTotal() {
      //reduce() 方法对数组中的每个元素按序执行一个 reducer 函数，每一次运行 reducer 会将先前元素的计算结果作为参数传入，
      // 最后将其结果汇总为单个返回值。
      return this.todos.reduce((preValue, currentValue) => preValue + (currentValue.done ? 1 : 0), 0)
    },
    /*
     doneTotal() {
       let count = 0
       this.todos.forEach((todo) => {
         if (todo.done) {
           count++
         }
       })
       return count
     },
    */
    //判断是否全选
    // isAll() {
    //   return (this.doneTotal === this.total && this.doneTotal > 0)
    // }
    isAll:{
      get(){
        return (this.doneTotal === this.total && this.doneTotal > 0)
      },
      set(value){
        this.checkAllTodo(value)
      }
    },

    },

  methods: {
  //   //全选/全不选
  //   checkAll(e) {
  //     this.checkAllTodo(e.target.checked)
  //   }
    clearAll(){
      if(confirm('你确定要删除已选中的任务嘛？')){
        this.deleteAllTodo()
      }
    }
  },

}
</script>

<style scoped>
/*footer*/
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

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}
</style>