<template>
  <li>
    <div class="header">
      <h3>{{ title }}</h3>
      <base-button variant="danger" size="sm">Delete</base-button>
    </div>
    <div :class="priorityClasses"></div>
  </li>
</template>

<script>
import BaseButton from './UI/BaseButton.vue';

export default {
  components: { BaseButton },
  props: {
    id: {
      type: String,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    description: {
      type: String,
      required: true
    },
    priority: {
      type: String,
      required: true
    }
  },
  computed: {
    priorityClasses() {
      const classes = ['priority'];
      switch (this.priority) {
        case 'normal':
          classes.push('normal');
          break;
        case 'important':
          classes.push('important');
          break;
        case 'urgent':
          classes.push('urgent');
          break;
        default:
      }
      return classes.join(' ');
    }
  }
};
</script>

<style scoped>
li {
  font-family: 'Space Grotesk', sans-serif;
  background-color: white;
  padding: 10px;
  color: #565656;
  border-radius: 4px;
  box-shadow: 0px 0px 3px rgba(0, 0, 0, 0.1);
  margin: 5px auto;
  cursor: pointer;
}

.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

li h3 {
  font-size: 1.1em;
}
.priority {
  height: 8px;
  width: 40px;
  border-radius: 20px;
  margin-top: 10px;
}

.priority.normal {
  background-color: #b2ffa9;
}

.priority.important {
  background-color: orange;
}

.priority.urgent {
  background-color: #ed474a;
}
</style>
