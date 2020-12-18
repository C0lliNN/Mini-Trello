<template>
  <section>
    <h2>{{ title }}</h2>
    <div class="container">
      <div class="background"></div>
      <div class="content">
        <draggable
          :list="todos"
          item-key="id"
          tag="transition-group"
          group="todos"
          class="list-group"
          v-bind="dragOptions"
          :component-data="{
            tag: 'ul',
            type: 'transition-group',
            name: !dragging ? 'flip-list' : null
          }"
          @change="handleChange"
          @start="dragging = true"
          @end="dragging = false"
        >
          <template #item="{ element, index }">
            <todos-list-item
              :key="index"
              v-bind="element"
              @click="$emit('handle-show-details-modal', element.id)"
              @handleDeleteTodo="deleteTodo(element.id)"
            >
            </todos-list-item>
          </template>
        </draggable>
      </div>
    </div>
  </section>
</template>

<script>
import draggable from 'vuedraggable';
import TodosListItem from './TodosListItem.vue';

export default {
  components: { TodosListItem, draggable },
  emits: [
    'handle-show-details-modal',
    'handle-delete-todo',
    'handle-change-list'
  ],
  props: {
    todos: {
      type: Array,
      required: false,
      default: () => []
    },
    title: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      dragging: false
    };
  },
  computed: {
    dragOptions() {
      return {
        animation: 200,
        group: "description",
        disabled: false,
        ghostClass: "ghost"
      };
    }
  },
  methods: {
    deleteTodo(id) {
      this.$emit('handle-delete-todo', id);
    },
    handleChange() {
      this.$emit('handle-change-list');
    }
  }
};
</script>

<style scoped>
section {
  min-width: 350px;
  padding: 20px;
  box-sizing: border-box;
}

section h2 {
  font-family: 'Space Grotesk', sans-serif;
  text-align: center;
  color: #565656;
}

.container {
  position: relative;
  height: 80vh;
  border: 1px solid #eee;
  border-radius: 4px;

  margin-top: 15px;
  box-sizing: border-box;
  box-shadow: 0px 0px 3px rgba(0, 0, 0, 0.1);
  overflow-y: auto;
  overflow-x: hidden;
}

.background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgb(242, 242, 242);
  background: linear-gradient(
    90deg,
    rgba(242, 242, 242, 1) 0%,
    rgba(245, 245, 245, 1) 100%
  );
}

.content {
  position: absolute;
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
  z-index: 10;
}

.content p {
  font-family: 'Space Grotesk', sans-serif;
  color: #565656;
  text-align: center;
  font-size: 1.05em;
}

.content ul {
  list-style: none;
}

.container::-webkit-scrollbar {
  width: 5px;
}

.container::-webkit-scrollbar-thumb {
  background: #666;
  border-radius: 50px;
}

.container::-webkit-scrollbar-track {
  background: #ddd;
  border-radius: 50px;
}

.no-move {
  transition: transform 0s;
}

.ghost {
  opacity: 0.5;
  background: #e6e6e6;
}

.list-group {
  padding-bottom: 65px;
}
</style>
