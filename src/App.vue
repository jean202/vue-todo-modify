<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo" @editTodo="editTodo" @saveTodo="saveTodo"></TodoList>
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
    return{
      todoItems:[],
      index:''
    }
  },
  created(){
        if(localStorage.length > 0){
            for(var i = 0; i < localStorage.length; i++){
                this.todoItems.push(localStorage.key(i));
            }
        }
    },
  methods: {
    clearAll(){
      localStorage.clear();
      this.todoItems = [];
    },
    addTodo(todoItem){
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    removeTodo(todoItem,index){
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1);
    },
    editTodo(todoItem,index){  
     localStorage.removeItem(todoItem);
     this.index = index;
    },
    saveTodo(todoItem){
      var editTodoItem = todoItem;
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.splice(this.index,1);
      this.todoItems.push(todoItem);
    }
  },
  components:{
    'TodoHeader':TodoHeader,
    'TodoInput':TodoInput,
    'TodoList':TodoList,
    'TodoFooter':TodoFooter
  }
}
</script>

<style>
  body{
    text-align:center;
    background-color:#F6F6F6;
  }
  input{
    border-radius: 5px;
    width:200px;
    
    background:white;
    text-align: center;
  }
  button{
   
    border-radius:5px;
  }
  .shadow{
    box-shadow: 5px 10px 10px rgba(0,0,0,0.03)
  }
  .header{
    font-size:20px;
    color:#8763FB;
    font-weight: bold;
  }
</style>