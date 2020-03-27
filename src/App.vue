<template>
  <div id="app">
    <h1>ToDo List</h1>
    <hr>
    <v-add-todo @createTodo="createTodo"></v-add-todo>
    <select v-model="filter">
      <option value="all">all</option>
      <option value="completed">completed</option>
      <option value="notcompleted">notcompleted</option>
    </select>
    <v-loader v-if="this.loading"></v-loader>
    <v-todo-list :todos="filteredSelect" @isDone="isDone" v-else-if="todos.length"></v-todo-list>
    <p v-else>there is no todos</p>
  </div>
</template>

<script>
import vTodoList from './components/todolist/v-todo-list';
import vAddTodo from './components/addtodo/v-add-todo';
import vLoader from './components/loader/v-loader';



export default {
  name: 'App',
  components: {
    vTodoList,
    vAddTodo,
    vLoader
  },
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  computed: {
    filteredSelect() {
      if(this.filter === 'all') {
        return this.todos
      }
      if(this.filter === 'completed') {
        return this.todos.filter(t => t.completed)
      }
      if(this.filter === 'notcompleted') {
        return this.todos.filter(t => !t.completed)
      }
    }
  },
  methods: {
    isDone(id) {
      this.todos = this.todos.filter(i => i.id !== id)
    },
    createTodo(todo) {
    this.todos.push(todo)
    }
  },
  async mounted() {
    const res = await fetch('https://jsonplaceholder.typicode.com/todos/1')
    const item = await res.json()
    setTimeout(() => {
      this.todos.push(item)
      this.loading = false
    }, 1000)

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
