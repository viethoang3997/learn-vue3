<template>
  <AddTodo @add-todo="addTodo" />
  <TodoItem v-for="todo in todos" :key="todo.id" :todoProps="todo"
  @item-completed="markCompleted"
  @delete-item="deleteItem">{{ todo }}</TodoItem>
  
</template>

<script>
import { ref } from 'vue'
import TodoItem from './TodoItem.vue'
import AddTodo from './AddTodo.vue'

import axios from 'axios'
export default {
  name: 'Todos',
  components: {
    TodoItem, AddTodo
  },
  setup() {
    const todos = ref([])
    const getData = async () => {
      try {
        const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
        todos.value = res.data
        // console.log(res.data)  
      } catch(error) {
        console.log(error)
      }
    }

    getData()

    const markCompleted = id => {
      //todos ko phai array ma la cai ref coi nhu la cai hop
      todos.value = todos.value.map(todo => {
        if(todo.id === id) todo.completed =! todo.completed
        return todo
      })
      // ham map: ham bac cao bien doi ham array bang cach chay qua lan luot tung phan tu cua array
    }

    const deleteItem = async id => {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        todos.value = todos.value.filter(todo => todo.id !== id)
      } catch(error) {
        console.log(error)
      }
    }

    const addTodo = async newTodo => {
      try {
        const res = await axios.post('https://jsonplaceholder.typicode.com/todos', newTodo)
        todos.value.push(res.data)
      } catch(error) {
        console.log(error)
      }
    }

    return {
      todos,
      markCompleted,
      deleteItem,
      addTodo,
    }
  }
   
}
</script>

<style>

</style>