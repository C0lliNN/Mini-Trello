<template>
  <h2>{{ title }}</h2>
  <ul v-if="todos.length">
    <li :key="todo.id" v-for="todo in todos">
      {{ todo.title }}
    </li>
  </ul>
  <p v-else>Sem Todos</p>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      required: false,
      default: () => []
    },
    title: {
      type: String,
      required: true
    }
  }
}
</script>