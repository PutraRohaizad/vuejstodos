<template>
  <div id="app">
      <Header/>  
      <AddTodo v-on:add-todo="addTodo" />
      <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Header from "./components/layout/Header"
import Todos from "./components/Todos"
import AddTodo from "./components/AddTodo"

export default {
  name: 'App',
  components: {
      Header,
      Todos,
      AddTodo
  },

  // Static Data
  data(){
      return {
       todos: [
         {
           id:1,
           title: "One",
           completed: false
         },
          {
           id:2,
           title: "two",
           completed: false
         },
          {
           id:3,
           title: "three",
           completed: false
         },
       ]
      }
  },
  // Function
  methods:{
    deleteTodo(id){
      // Filter show all data except the id that has been clicked
      this.todos = this.todos.filter(todo => todo.id !== id)
    },

    addTodo(newTodo){
      this.todos = [...this.todos, newTodo];
    }
  }

}
</script>

<style>

</style>
