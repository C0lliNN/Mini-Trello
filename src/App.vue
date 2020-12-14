<template>
  <the-header @handleShowCreateModal="showCreateModal"></the-header>
  <main>
    <todos-list title="Todo" :todos="pendingTodos"></todos-list>
    <todos-list title="Done"></todos-list>
  </main>
  <create-todo-item @handleCloseModal="closeCreateModal" :showModal="showCreateTodoModal"></create-todo-item>
</template>

<script>
import CreateTodoItem from './components/CreateTodoItem.vue';
import TheHeader from './components/TheHeader';
import TodosList from './components/TodosList';

export default {
  name: 'App',

  components: {
    TheHeader,
    TodosList,
    CreateTodoItem
  },
  data() {
    return {
      pendingTodos: [
        {
          id: '1',
          title: 'Todo Test',
          description: 'Todo Description',
          priority: 'Normal'
        },
        {
          id: '2',
          title: 'Todo Test',
          description: 'Todo Description',
          priority: 'Normal'
        }
      ],
      doneTodos: [],
      showCreateTodoModal: false
    };
  },
  methods: {
    showCreateModal() {
      this.showCreateTodoModal = true;
    },
    closeCreateModal() {
      this.showCreateTodoModal = false;
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
