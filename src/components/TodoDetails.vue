<template>
  <base-modal>
    <template #header>
      <h3>Detalhes do Todo</h3>
    </template>
    <template #body>
      <base-form-group>
        <label for="title">Título</label>
        <input
          type="text"
          id="title"
          autocomplete="off"
          :value="title"
          readonly
        />
      </base-form-group>
      <base-form-group>
        <label for="description">Descrição</label>
        <textarea
          id="description"
          rows="10"
          autocomplete="off"
          :value="description"
          readonly
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
              disabled
              :checked="priority === 'normal'"
            />
            <div class="normal"></div>
          </label>
          <label class="priority">
            <input
              type="radio"
              name="priority"
              value="important"
              disabled
              :checked="priority === 'important'"
            />
            <div class="important"></div>
          </label>
          <label class="priority">
            <input
              type="radio"
              name="priority"
              value="urgent"
              disabled
              :checked="priority === 'urgent'"
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
      <base-button variant="primary">OK</base-button>
    </template>
  </base-modal>
</template>

<script>
import BaseModal from './UI/BaseModal';
import BaseButton from './UI/BaseButton';
import BaseFormGroup from './UI/BaseFormGroup';

export default {
  components: { BaseModal, BaseFormGroup, BaseButton },
  emits: ['handle-close-modal'],
  props: {
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
  }
};
</script>
