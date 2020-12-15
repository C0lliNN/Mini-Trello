<template>
  <base-modal :showModal="showModal">
    <template #header>
      <h3>Detalhes do Todo</h3>
    </template>
    <template #body>
      <base-form-group>
        <label for="title2">Título</label>
        <input
          type="text"
          id="title2"
          autocomplete="off"
          v-model="titleValue"
          :readonly="!editMode"
        />
      </base-form-group>
      <base-form-group>
        <label for="description2">Descrição</label>
        <textarea
          id="description2"
          rows="10"
          autocomplete="off"
          :readonly="!editMode"
          v-model="descriptionValue"
        ></textarea>
      </base-form-group>
      <div class="priority-group">
        <label>Prioridade</label>
        <div>
          <label class="priority">
            <input
              type="radio"
              name="priority"
              value="normal"
              :disabled="!editMode"
              v-model="priorityValue"
            />
            <div class="normal"></div>
          </label>
          <label class="priority">
            <input
              type="radio"
              name="priority"
              value="important"
              :disabled="!editMode"
              v-model="priorityValue"
            />
            <div class="important"></div>
          </label>
          <label class="priority">
            <input
              type="radio"
              name="priority"
              value="urgent"
              :disabled="!editMode"
              v-model="priorityValue"
            />
            <div class="urgent"></div>
          </label>
        </div>
      </div>
    </template>
    <template #footer>
      <base-button
        style="margin-right: 10px"
        variant="danger"
        @click="$emit('handle-close-modal')"
      >
        Fechar
      </base-button>
      <base-button
        variant="primary"
        @click="editMode ? saveTodo() : setEditMode()"
      >
        {{ editMode ? 'Salvar' : 'Editar' }}
      </base-button>
    </template>
  </base-modal>
</template>

<script>
import BaseModal from './UI/BaseModal';
import BaseButton from './UI/BaseButton';
import BaseFormGroup from './UI/BaseFormGroup';

export default {
  components: { BaseModal, BaseFormGroup, BaseButton },
  emits: ['handle-close-modal', 'handle-save-todo'],
  props: {
    id: {
      type: String,
      required: false
    },
    title: {
      type: String,
      required: false
    },
    description: {
      type: String,
      required: false
    },
    priority: {
      type: String,
      required: false
    },
    showModal: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      titleValue: this.title,
      descriptionValue: this.description,
      priorityValue: this.priority,
      editMode: false
    };
  },
  watch: {
    title(val) {
      this.titleValue = val;
    },
    description(val) {
      this.descriptionValue = val;
    },
    priority(val) {
      this.priorityValue = val;
    },
    showModal(val) {
      if(!val) {
        this.editMode = false;
      }
    }
  },
  methods: {
    setEditMode() {
      this.editMode = true;
    },
    saveTodo() {
      this.$emit(
        'handle-save-todo',
        this.id,
        this.titleValue,
        this.descriptionValue,
        this.priorityValue
      );
      this.editMode = false;
      this.$emit('handle-close-modal');
    }
  }
};
</script>
