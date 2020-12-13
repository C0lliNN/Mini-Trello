<template>
  <the-header></the-header>
  <main>
    <todos-list title="Todo" :todos="pendingTodos"></todos-list>
    <todos-list title="Done"></todos-list>
  </main>
</template>

<script>
import TheHeader from './components/TheHeader';
import TodosList from './components/TodosList';

export default {
  name: 'App',
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
      doneTodos: []
    };
  },
  components: {
    TheHeader,
    TodosList
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
