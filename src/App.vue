<template>
  <the-header @handleShowCreateModal="showCreateModal"></the-header>
  <main>
    <todos-list
      @handleShowDetailsModal="showDetails"
      @handleDeleteTodo="deleteTodo"
      title="Todo"
      :todos="pendingTodos"
    ></todos-list>
    <todos-list
      @handleShowDetailsModal="showDetails"
      title="Done"
      :todos="ongoingTodos"
      @handleDeleteTodo="deleteTodo"
    ></todos-list>
    <todos-list
      @handleShowDetailsModal="showDetails"
      title="Done"
      :todos="doneTodos"
      @handleDeleteTodo="deleteTodo"
    ></todos-list>
  </main>
  <create-todo-item
    @handleCloseModal="closeCreateModal"
    :showModal="showCreateTodoModal"
    @handleCreateTodo="addTodo"
  ></create-todo-item>
  <todo-details
    @handleCloseModal="closeDetailsModal"
    @handleSaveTodo="saveTodo"
    :showModal="!!selectedTodo"
    v-bind="selectedTodo"
  ></todo-details>
</template>

<script>
import CreateTodoItem from './components/CreateTodoItem.vue';
import TheHeader from './components/TheHeader';
import TodosList from './components/TodosList';
import TodoDetails from './components/TodoDetails';

const LOCAL_STORAGE_KEY = 'MINI_TRELO:DATA';

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
      pendingTodos: [],
      ongoingTodos: [],
      doneTodos: [],
      showCreateTodoModal: false,
      selectedTodo: null
    };
  },
  mounted() {
    const data = JSON.parse(localStorage.getItem(LOCAL_STORAGE_KEY));

    if (data) {
      this.pendingTodos = data.pendingTodos;
      this.ongoingTodos = data.ongoingTodos;
      this.doneTodos = data.doneTodos;
    }
  },
  methods: {
    showCreateModal() {
      this.showCreateTodoModal = true;
    },
    closeCreateModal() {
      this.showCreateTodoModal = false;
    },
    showDetails(id) {
      const todo = this.getTodo(id);
      this.selectedTodo = todo;
    },
    saveTodo(id, title, description, priority) {
      const todo = this.getTodo(id);
      todo.title = title;
      todo.description = description;
      todo.priority = priority;
      this.updateLocalStorage();
    },
    deleteTodo(id) {
      let index = this.pendingTodos.findIndex((p) => p.id === id);
      if (index >= 0) {
        this.pendingTodos.splice(index, 1);
      } else {
        index = this.doneTodos.findIndex((p) => p.id === id);
        this.doneTodos.splice(index, 1);
      }
      this.updateLocalStorage();
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
      this.updateLocalStorage();
    },
    getTodo(id) {
      let el = this.pendingTodos.find((p) => p.id === id);
      if (!el) {
        el = this.doneTodos.find((p) => p.id === id);
      }
      return el;
    },
    updateLocalStorage() {
      localStorage.setItem(
        LOCAL_STORAGE_KEY,
        JSON.stringify({
          pendingTodos: this.pendingTodos,
          ongoingTodos: this.ongoingTodos,
          doneTodos: this.doneTodos
        })
      );
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
