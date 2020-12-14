<template>
  <section>
    <h2>{{ title }}</h2>
    <div class="card">
      <ul v-if="todos.length">
        <todos-list-item
          :key="todo.id"
          v-for="todo in todos"
          v-bind="todo"
          @click="$emit('handle-show-details-modal', todo)"
        >
        </todos-list-item>
      </ul>
      <p v-else>Sem Todos</p>
    </div>
  </section>
</template>

<script>
import TodosListItem from './TodosListItem.vue';
export default {
  components: { TodosListItem },
  emits: ['handle-show-details-modal'],
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
};
</script>

<style scoped>
section {
  width: 40%;
  min-width: 400px;
  margin: 20px auto;
}

section h2 {
  font-family: 'Space Grotesk', sans-serif;
  text-align: center;
  color: #565656;
}

.card {
  border: 1px solid #eee;
  border-radius: 8px;
  background-color: rgba(30, 30, 30, 0.1);
  height: 70vh;
  padding: 20px;
  margin-top: 15px;
  box-sizing: border-box;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.3);
  overflow-y: auto;
}

.card p {
  font-family: 'Space Grotesk', sans-serif;
  color: #565656;
  text-align: center;
  font-size: 1.05em;
}

section ul {
  list-style: none;
}
</style>
