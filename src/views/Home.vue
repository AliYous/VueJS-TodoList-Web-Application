<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo'
import axios from 'axios'


export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos : []
    }
  },
  methods: {
    //We could do this in multiple ways, here we basically just filter the todos and keep only those where the id != id of the deleted todo
    deleteTodo(todoId) {
      axios.delete('https://jsonplaceholder.typicode.com/todos/${todoId}')
      .then(this.todos = this.todos.filter(todo => todo.id !== todoId))
      .catch(err => console.log(err))
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo; //use destrcuturing to pull out title and completed from the newTodo object
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
      .then(res => this.todos = [...this.todos, res.data])
      .catch(err => console.log(err))
    }
  },
  
  created() { //Similar to TypeScript onInit()
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res => this.todos = res.data)
    .catch(err => console.log(err))
  }
}
</script>

<style>

</style>
