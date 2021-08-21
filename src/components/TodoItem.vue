<template>
  <p :class="['todo-item', todoProps.completed ? 'is-completed' : '']">
    <input type="checkbox" :checked="todoProps.completed"/>
    {{ todoProps.title }}
    <button class="del-btn">Delete</button>
  </p>
</template>

<script>
export default {
  name: 'TodoItem',
  props: ['todoProps']
}
</script>

<style scope>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  margin: 0;
  border-bottom: 1px #ccc dotted;
}

.is-completed {
  text-decoration: line-through;
}

.del-btn {
  background-color: crimson;
  color: white;
  border: none;
  cursor: pointer;
  float: right;
}
</style>