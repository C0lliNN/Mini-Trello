<template>
  <div :class="classes">
    <div class="modal">
      <div class="modal-header">
        <slot name="header"></slot>
      </div>
      <div class="modal-body">
        <slot name="body"></slot>
      </div>
      <div class="modal-footer" v-if="$slots.footer">
        <slot name="footer"></slot>
      </div>
    </div>
    <div class="backdrop"></div>
  </div>
</template>

<script>
export default {
  props: {
    showModal: {
      type: Boolean,
      required: true,
    }
  },
  computed: {
    classes() {
      const classesArray = ['modal-dialog'];
      if (this.showModal) {
        classesArray.push('show');
      }
      return classesArray.join(' ');
    }
  }
}
</script>

<style scoped>
.modal-dialog {
  position: absolute;
  width: 100%;
  height: 100%;
  left: -100%;
  
}

.modal-dialog.show {
  display: flex;
  align-items: center;
  justify-content: center;
  top: 0;
  left: 0;
}

.backdrop {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(48, 48, 48, 0.5);
  z-index: 10;
  opacity: 0;
  transition: opacity 0.3s ease-in-out;
}

.show .backdrop {
  opacity: 1;
}

.modal {
  width: 70%;
  min-width: 350px;
  background-color: white;
  border-radius: 12px;
  z-index: 100;
  box-sizing: border-box;
  position: relative;
  transform: translateY(-600%);
  transition: transform 0.5s ease-in-out;
  transition-delay: 0.3s;
}

.show .modal {
  transform: translateY(0);
}

.modal-header {
  position: absolute;
  height: 54px;
  width: 100%;
  border-bottom: 1px solid #ddd;
  display: flex;
  align-items: center;
  box-sizing: border-box;
  background-color: #565656;
  padding: 0 20px;
  border-top-left-radius: 12px;
  border-top-right-radius: 12px;
  color: white;
  font-family: 'Space Grotesk', sans-serif;
}

.modal-body {
  padding: 74px 20px;
  box-sizing: border-box;
  font-family: 'Space Grotesk', sans-serif;
}

.modal-footer {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;
  height: 54px;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  border-top: 1px solid #56565669;
}
</style>
