<template>
  <div class="form-group">
    <slot></slot>
  </div>
</template>

<style>
.form-group {
  margin-bottom: 10px;
}

.form-group input,
.form-group textarea {
  display: block;
  width: 100%;
  margin-top: 5px;
  outline: none;
  border: none;
  padding: 10px;
  border-radius: 4px;
  border: 1px solid #ddd;
  box-sizing: border-box;
  transition: box-shadow 0.2s ease-in-out;
}
.form-group input:focus,
.form-group textarea:focus {
  box-shadow: 0px 0px 0px 3px #56565634;
}
</style>
