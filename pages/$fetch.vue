<script setup>
const completed = ref('false');

const todos = await $fetch('https://jsonplaceholder.typicode.com/todos', {
  params: {
    completed: completed.value,
  },
});
console.log('Count:', todos.length);
</script>

<template>
  <div>
    <div v-for="(todo, i) in todos" :key="i">
      <input type="checkbox" v-model="todo.completed" />
      {{ todo.title }}
    </div>
  </div>
</template>
