<template>
  <base-modal :showModal="showModal">
    <template #header>
      <h3>
        Novo Todo
      </h3>
    </template>
    <template #body>
      Teste
    </template>
    <template #footer>
      <base-button variant="danger" @click="$emit('handle-close-modal')">
        Cancelar
      </base-button>
    </template>
  </base-modal>
</template>

<script>
import BaseButton from './UI/BaseButton.vue'
import BaseModal from './UI/BaseModal'

export default {
  emits: ['handle-close-modal'],
  props: ['showModal'],
  components: {
    BaseModal,
    BaseButton
  }
}
</script>