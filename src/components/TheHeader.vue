<template>
  <header>
    <h1>
      <img src="../assets/icon.png" alt="" width="40">
      <span>Mini Trello</span> 
    </h1>
    <base-button @click="$emit('handle-show-create-modal')" variant="success"
      >Novo</base-button
    >
  </header>
</template>

<script>
import BaseButton from './UI/BaseButton';

export default {
  components: {
    BaseButton
  }
};
</script>

<style scoped>
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #565656;
  padding: 10px 40px;
  box-sizing: border-box;
  box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
}
h1 {
  font-family: 'Space Grotesk', sans-serif;
  color: #ffffff;
  display: flex;
  align-items: center;
}

img {
  margin-right: 10px;
}
</style>
