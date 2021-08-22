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
import {v4 as uuidv4} from 'uuid'
export default {
  name: 'Todos',
  components: {
    TodoItem, AddTodo
  },
  setup() {
    const todos = ref([
      {
        id: uuidv4(),
        title: 'Việc 1',
        completed: false
      },
      {
        id: uuidv4(),
        title: 'Việc 2',
        completed: false
      }, 
      {
        id: uuidv4(),
        title: 'Việc 3',
        completed: false
      }  
    ])
  
    const markCompleted = id => {
      //todos ko phai array ma la cai ref coi nhu la cai hop
      todos.value = todos.value.map(todo => {
        if(todo.id === id) todo.completed =! todo.completed
        return todo
      })
      // ham map: ham bac cao bien doi ham array bang cach chay qua lan luot tung phan tu cua array
    }

    const deleteItem = id => {
      todos.value = todos.value.filter(todo => todo.id !== id)
    }

    const addTodo = newTodo => {
      todos.value.push(newTodo)
    }

    return {
      todos,
      markCompleted,
      deleteItem,
      addTodo
    }
  }
   
}
</script>

<style>

</style>