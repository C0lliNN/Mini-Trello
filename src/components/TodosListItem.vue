<template>
  <li>
    <div class="header">
      <h3>{{ title }}</h3>
      <base-button variant="danger" size="sm" @click="deleteTodo(id)">
        <svg class="svg-icon" viewBox="0 0 20 20">
          <path
            d="M17.114,3.923h-4.589V2.427c0-0.252-0.207-0.459-0.46-0.459H7.935c-0.252,0-0.459,0.207-0.459,0.459v1.496h-4.59c-0.252,0-0.459,0.205-0.459,0.459c0,0.252,0.207,0.459,0.459,0.459h1.51v12.732c0,0.252,0.207,0.459,0.459,0.459h10.29c0.254,0,0.459-0.207,0.459-0.459V4.841h1.511c0.252,0,0.459-0.207,0.459-0.459C17.573,4.127,17.366,3.923,17.114,3.923M8.394,2.886h3.214v0.918H8.394V2.886z M14.686,17.114H5.314V4.841h9.372V17.114z M12.525,7.306v7.344c0,0.252-0.207,0.459-0.46,0.459s-0.458-0.207-0.458-0.459V7.306c0-0.254,0.205-0.459,0.458-0.459S12.525,7.051,12.525,7.306M8.394,7.306v7.344c0,0.252-0.207,0.459-0.459,0.459s-0.459-0.207-0.459-0.459V7.306c0-0.254,0.207-0.459,0.459-0.459S8.394,7.051,8.394,7.306"
          ></path>
        </svg>
      </base-button>
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
  emits: ['handle-delete-todo'],
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
  },
  deleteTodo(id) {
    this.$emit('handle-delete-todo', id);
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

li:hover {
  background-color: #f8f6f6;
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

.svg-icon {
  width: 1.6em;
  height: 1.6em;
}

.svg-icon path,
.svg-icon polygon,
.svg-icon rect {
  fill: #fff;
}

.svg-icon circle {
  stroke: #fff;
  stroke-width: 1;
}
</style>
