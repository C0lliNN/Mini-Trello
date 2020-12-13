<template>
  <the-header></the-header>
  <Todos title="Todo"/>
</template>

<script>
import TheHeader from './components/TheHeader';
import Todos from './components/Todos';

export default {
  name: 'App',
  components: {
    TheHeader,
    Todos
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
</style>
