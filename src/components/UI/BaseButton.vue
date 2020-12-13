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
    },
    size: {
      type: String,
      required: false,
      default: '',
    }
  },
  computed: {
    classes() {
      const classes = ['btn'];

      if (this.variant === 'success') {
        classes.push('btn-success');
      }

      if (this.variant === 'danger') {
        classes.push('btn-danger');
      }

      if (this.size === 'sm') {
        classes.push('btn-sm');
      }

      return classes.join(' ');
    }
  }
};
</script>

<style scoped>
.btn {
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

.btn-success {
  background-color: #b2ffa9;
}

.btn-sucesss:hover {
  background-color: #a3ff99;
}

.btn-danger {
  background-color: #ed474a;
  color: white;
}

.btn-danger:hover {
  background-color: #ee585a;
}

.btn-sm {
  padding: 7px 12px;
  font-size: 0.9em;
  font-weight: 500;
}
</style>
