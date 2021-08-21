<template>
  <TodoItem v-for="todo in todos" v-bind:key="todo.id" v-bind:todoProps="todo">{{ todo }}</TodoItem>
  
</template>

<script>
import TodoItem from './TodoItem.vue'
export default {
  name: 'Todos',
  components: {
    TodoItem,
  },
 
  data() {
    return {
      todos: [
        {
          id: 1,
          title: 'Việc 1',
          completed: true
        },
        {
          id: 2,
          title: 'Việc 2',
          completed: false
        }, 
        {
          id: 3,
          title: 'Việc 3',
          completed: false
        }  
      ],
    }
  }
  
}
</script>

<style>

</style>