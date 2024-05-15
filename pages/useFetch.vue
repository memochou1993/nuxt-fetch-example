<script setup>
const completed = ref('false');

const { data: todos, error, refresh } = await useFetch('https://jsonplaceholder.typicode.com/todos', {
  params: {
    completed: completed, // without ".value"
  },
  // watch: false, // Disable watching for changes
  // immediate: false, // Do not fetch immediately
  // server: false, // Do not fetch on server-side
});
if (error.value) {
  // Handle error
  console.log(error);
}
console.log('[useFetch] TODO Count:', todos.value?.length);

await useFetch('https://hub.dummyapis.com/delay?seconds=1', {
  // lazy: true, // Resolve async function after loading the route
});
</script>

<template>
  <div>
    <form>
      Completed:
      <input type="radio" v-model="completed" value="true" />Yes
      <input type="radio" v-model="completed" value="false" />No
      <input type="button" @click="refresh" value="Refresh" />
    </form>
    <div v-for="(todo, i) in todos" :key="i">
      <input type="checkbox" v-model="todo.completed" />
      {{ todo.title }}
    </div>
  </div>
</template>
