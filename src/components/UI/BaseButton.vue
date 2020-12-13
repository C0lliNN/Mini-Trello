<template>
  <button :class="classes">
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: {
    variant: {
      type: String,
      required: true
    }
  },
  computed: {
    classes() {
      if (this.variant === 'success') {
        return 'success';
      }
      return '';
    }
  }
};
</script>

<style scoped>
button {
  border: none;
  outline: none;
  color: #565656;
  padding: 10px 20px;
  border-radius: 4px;
  font-size: 1.05em;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.2s ease-in;
}

.success {
  background-color: #b2ffa9;
}

.sucesss:hover {
  background-color: #a3ff99;
}
</style>
