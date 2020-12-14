<template>
  <header>
    <h1>
      Todos
    </h1>
    <button>Novo</button>
  </header>
</template>

<style scoped>
  header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: #ffc85c;
    padding: 10px 40px;
    box-sizing: border-box;
    box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
  }
  h1 {
    font-family: 'Space Grotesk', sans-serif;
    color: #ffffff;
  }
  button {
    border: none;
    outline: none;
    background-color: #59886b;
    color: white;
    padding: 10px 20px;
    border-radius: 4px;
    font-size: 1.05em;
    font-weight: bold;
    cursor: pointer;
  }
</style>
