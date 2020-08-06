<template>
  <div>
    <h1>Todo Application</h1>
    <router-link to="/">Home</router-link>
    <hr/>
    <select v-model="filtering">
      <option value="all">all</option>
      <option value="completed">completed</option>
      <option value="not-completed">not-completed</option>
    </select>
    <hr/>
    <AddTodo
        @add-todo="addTodo"
    />
    <hr/>
    <Loader
        v-if="loadingTodos"
    />
    <TodoList
        v-else-if="filteredTodos.length"
        v-bind:todos="filteredTodos"
        @remove-todo="removeTodo"
    />
    <p v-else>No Todos!</p>
  </div>
</template>


<script>

import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'

export default {
  name: 'App',
  data() {
    return {
      todos: [
        // {id: 1, title: 'Buy some milk', completed: false},
        // {id: 2, title: 'Buy some coffee', completed: false},
        // {id: 3, title: 'Buy some sugar', completed: false},
        // {id: 4, title: 'Buy some whisky', completed: false}
      ],
      loadingTodos: true,
      filtering: 'all'
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
        .then(response => response.json())
        .then(json => {
          setTimeout(() => {
            this.todos = json
            this.loadingTodos = false
          }, 1500)
        })
  },
  // watch: {
  //   filter(value){
  //     console.log(value)
  //   }
  // },
  computed:{
    filteredTodos(){
        if (this.filtering === 'all') {
          return this.todos
        }
        if (this.filtering === 'completed') {
          return  this.todos.filter(t => t.completed)
        }
        if (this.filtering === 'non-completed') {
          return  this.todos.filter(t => !t.completed)
        }
    }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  components: {
    TodoList, AddTodo, Loader
  }
}
</script>