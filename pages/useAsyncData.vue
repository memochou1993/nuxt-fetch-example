<script setup>
const completed = ref('false');

const { data: todos, error } = await useAsyncData('todos', () => $fetch('https://jsonplaceholder.typicode.com/todos', {
  params: {
    completed: completed.value,
  },
}));
if (error.value) {
  // Handle error
  console.log(error);
}
console.log('Count:', todos.value.length);
</script>

<template>
  <div>
    <div v-for="(todo, i) in todos" :key="i">
      <input type="checkbox" v-model="todo.completed" />
      {{ todo.title }}
    </div>
  </div>
</template>
