<template>
  <form @submit="addItem">
    <input type="text" class="content" placeholder="Thêm công việc của bạn" v-model="title">
    <input type="submit" value="Thêm" class="add-btn">
  </form>
</template>

<script>
import { ref } from 'vue'
import {v4 as uuidv4} from 'uuid'
export default {
  name: 'AddTodo',
  setup(props, context) {
    const title = ref('')

    const addItem = event => {
      event.preventDefault()

      const newItem = {
        id: uuidv4,
        title: title.value,
        completed: false
      }
      context.emit('add-todo', newItem)
      title.value = ''
    } 

    return {
      title,
      addItem
    }
  }
}
</script>

<style>
form {
  display:flex;
}

.content {
  flex: 10;
  padding: 5px;
}

.add-btn {
  flex: 2;
}
</style>