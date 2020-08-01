<template>
  <div>
      <form @submit="addTodo">
          <input class="input" v-model="title" type="text" name="title" placeholder="Todo..">
          <input class="btn" type="submit" value="Submit"/>
      </form>
  </div>
</template>

<script>
// import { v4 as uuidv4 } from "uuid"
export default {
    name:"AddTodo",
    data(){
        return{
            title:''
        }
    },
    methods:{
        addTodo(e){
            e.preventDefault()
            const newTodo = {
                title: this.title,
                completed: false
            }
            // send up to parent
            this.$emit('add-todo', newTodo);
            this.title = '';
        }
    }
}
</script>

<style scoped>
    form{
        display: flex;
    }

    .input{
        flex: 10;
        padding: 5px;
    }

    .btn{
        display: inline-block;
        background: rgb(137, 183, 236);
        padding: 1rem;
        cursor: pointer;
        color: white;
    }

    .btn:hover{
        background: white;
        color:rgb(137, 183, 236);
    }
</style>