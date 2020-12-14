<template>
  <the-header @handleShowCreateModal="showCreateModal"></the-header>
  <main>
    <todos-list
      @handleShowDetailsModal="showDetails"
      title="Todo"
      :todos="pendingTodos"
    ></todos-list>
    <todos-list @handleShowDetailsModal="showDetails" title="Done"></todos-list>
  </main>
  <create-todo-item
    @handleCloseModal="closeCreateModal"
    :showModal="showCreateTodoModal"
    @handleCreateTodo="addTodo"
  ></create-todo-item>
  <todo-details
    @handleCloseModal="closeDetailsModal"
    :showModal="selectedTodo"
    v-bind="selectedTodo"
  ></todo-details>
</template>

<script>
import CreateTodoItem from './components/CreateTodoItem.vue';
import TheHeader from './components/TheHeader';
import TodosList from './components/TodosList';
import TodoDetails from './components/TodoDetails';

export default {
  name: 'App',

  components: {
    TheHeader,
    TodosList,
    CreateTodoItem,
    TodoDetails
  },
  data() {
    return {
      pendingTodos: [
        {
          id: '1',
          title: 'Todo Test',
          description: 'Todo Description',
          priority: 'normal'
        },
        {
          id: '2',
          title: 'Todo Test',
          description: 'Todo Description',
          priority: 'normal'
        }
      ],
      doneTodos: [],
      showCreateTodoModal: false,
      selectedTodo: null
    };
  },
  methods: {
    showCreateModal() {
      this.showCreateTodoModal = true;
    },
    closeCreateModal() {
      this.showCreateTodoModal = false;
    },
    showDetails(todo) {
      console.log(todo);
      this.selectedTodo = todo;
    },
    closeDetailsModal() {
      this.selectedTodo = null;
    },
    addTodo(title, description, priority) {
      this.pendingTodos.push({
        id: new Date().toISOString(),
        title,
        description,
        priority
      });
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

main {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}
</style>
