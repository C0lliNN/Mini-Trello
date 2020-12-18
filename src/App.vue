<template>
  <the-header @handleShowCreateModal="showCreateModal"></the-header>
  <main>
    <todos-list
      @handleShowDetailsModal="showDetails"
      @handleDeleteTodo="deleteTodo"
      title="Todo"
      :todos="pendingTodos"
      @handleChangeList="updateLocalStorage"
    ></todos-list>
    <todos-list
      @handleShowDetailsModal="showDetails"
      title="Doing"
      :todos="ongoingTodos"
      @handleDeleteTodo="deleteTodo"
      @handleChangeList="updateLocalStorage"
    ></todos-list>
    <todos-list
      @handleShowDetailsModal="showDetails"
      title="Done"
      :todos="doneTodos"
      @handleDeleteTodo="deleteTodo"
      @handleChangeList="updateLocalStorage"
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
      this.pendingTodos = data.pendingTodos ?? [];
      this.ongoingTodos = data.ongoingTodos ?? [];
      this.doneTodos = data.doneTodos ?? [];
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
      let array = this.pendingTodos;

      if (index < 0) {
        index = this.ongoingTodos.findIndex((p) => p.id === id);
        array = this.ongoingTodos;
      } 

      if (index < 0) {
        index = this.doneTodos.findIndex((p) => p.id === id);
        array = this.doneTodos;
      }

      array.splice(index, 1);

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
        el = this.ongoingTodos.find((p) => p.id === id);
      }
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
  flex-wrap: nowrap;
  overflow-x: auto;
  margin: 0 10px;
}

@media (min-width: 1200px) {
  main {
    justify-content: center;
  }
}

main::-webkit-scrollbar {
  height: 10px;
}

main::-webkit-scrollbar-thumb {
  background: #565656;
  border-radius: 20px;
}

main::-webkit-scrollbar-track {
  background: #ddd;
  border-radius: 20px;
}
</style>
