<template>
  <base-modal :showModal="showModal">
    <template #header>
      <h3>Novo Todo</h3>
    </template>
    <template #body>
      <base-form-group>
        <label for="title">Título</label>
        <input type="text" id="title" autocomplete="off" v-model="title" />
      </base-form-group>
      <base-form-group>
        <label for="description">Descrição</label>
        <textarea
          id="description"
          rows="5"
          autocomplete="off"
          v-model="description"
        ></textarea>
      </base-form-group>
      <div class="priority-group">
        <label>Prioridade</label>
        <div>
          <label class="priority">
            <input type="radio" name="priority" value="normal" v-model="priority"/>
            <div class="normal"></div>
          </label>
          <label class="priority">
            <input type="radio" name="priority" value="important" v-model="priority"/>
            <div class="important"></div>
          </label>
          <label class="priority">
            <input type="radio" name="priority" value="urgent" v-model="priority"/>
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
        Cancelar
      </base-button>
      <base-button variant="success"> Criar </base-button>
    </template>
  </base-modal>
</template>

<script>
import BaseButton from './UI/BaseButton.vue';
import BaseFormGroup from './UI/BaseFormGroup.vue';
import BaseModal from './UI/BaseModal';

export default {
  emits: ['handle-close-modal'],
  props: {
    showModal: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      title: '',
      description: '',
      priority: 'normal'
    };
  },
  components: {
    BaseModal,
    BaseButton,
    BaseFormGroup
  }
};
</script>

<style>
.priority input {
  display: none;
}

.priority input:checked + div {
  box-shadow: 0px 0px 0px 3px rgb(4, 175, 255);
}

.priority-group > div {
  display: flex;
  align-items: center;
  margin-top: 5px;
}

.normal,
.important,
.urgent {
  width: 60px;
  height: 30px;
  border-radius: 8px;
  cursor: pointer;
  border: 2px solid white;
  transition: box-shadow 0.3s ease-in-out;
}

.normal {
  background-color: #b2ffa9;
}

.important {
  background-color: orange;
  margin: 0 15px;
}

.urgent {
  background-color: #ed474a;
}
</style>
