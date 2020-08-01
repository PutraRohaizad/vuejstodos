<template>
  <div id="app" class="container">
      <Header/>  
      <AddTodo v-on:add-todo="addTodo" />
      <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Header from "./components/layout/Header"
import Todos from "./components/Todos"
import AddTodo from "./components/AddTodo"
import axios from "axios"

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
       todos: []
      }
  },

    // Use Axios
        // created(){
        //   axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
        //   .then(res=> this.todos =res.data)
        //   .catch(err => console.log(err));
        // },

    // use Fetch
      created(){
        fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
        .then(res => res.json())
        .then(data => {
          this.todos = data
        })
        .catch(err => console.log(err));
      },

  // Function
  methods:{
    deleteTodo(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        // Filter show all data except the id that has been clicked
      .then(res => {
      console.log(res);
      this.todos = this.todos.filter(todo => todo.id !== id)
      })
      .catch(err => console.log(err));

    },

    addTodo(newTodo){
      const { title , completed} = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title,
        completed
      })
      .then(res=>this.todos = [...this.todos, res.data])
      
    }
  }

}
</script>

<style>
  .container{
    margin: 5rem;
  }
</style>
