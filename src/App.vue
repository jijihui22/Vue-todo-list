<!--TodoHeader 어플리케이션 이름 표시
TodoInput 할일 입력 및 추가
TodoList 할일 목록 표시 및 특정 할일 삭제
TodoFooter 할일 모두 삭제-->
<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data(){
    return {
      todoItems:[]
    }
  },
  created(){
            if(localStorage.length > 0){
                for(let i = 0;i < localStorage.length;i++){
                    this.todoItems.push(localStorage.key(i));
                }
            }
        },
  methods:{
    addTodo(todoItem){
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    clearAll(){
      localStorage.clear();
      this.todoItems = [];
    },
    removeTodo(todoItem, index){
                localStorage.removeItem(todoItem);
                this.todoItems.splice(index, 1);
            }
  },
  components: {
    'TodoHeader' : TodoHeader,
    'TodoInput' : TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter
  }
}

</script>

<style>
body{
  font-family: 'Ubuntu', sans-serif;
  text-align: center;
  background-color: #f6f6f8;
}
input{
  border-style: groove;
  width: 200px;
}
button{
  border-style: groove;
}
.shadow{
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}
</style>