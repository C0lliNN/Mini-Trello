<template>
  <section>
    <h2>{{ title }}</h2>
    <div class="card">
      <ul v-if="todos.length">
        <todos-list-item
          :key="todo.id"
          v-for="todo in todos"
          v-bind="todo"
          @click="$emit('handle-show-details-modal', todo.id)"
          @handleDeleteTodo="deleteTodo(todo.id)"
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
  emits: ['handle-show-details-modal', 'handle-delete-todo'],
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
  },
  methods: {
    deleteTodo(id) {
      this.$emit('handle-delete-todo', id);
    }
  }
};
</script>

<style scoped>
section {
  min-width: 350px;
  padding: 20px;
  box-sizing: border-box;
}

section h2 {
  font-family: 'Space Grotesk', sans-serif;
  text-align: center;
  color: #565656;
}

.card {
  border: 1px solid #eee;
  border-radius: 4px;
  background-color: rgba(30, 30, 30, 0.05);
  height: 80vh;
  padding: 10px;
  margin-top: 15px;
  box-sizing: border-box;
  box-shadow: 0px 0px 3px rgba(0, 0, 0, 0.5);
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
