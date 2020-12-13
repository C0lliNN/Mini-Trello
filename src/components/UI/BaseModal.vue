<template>
  <div class="modal-dialog">
    <div class="modal">
      <div class="modal-header">
        <slot name="header"></slot>
      </div>
      <div class="modal-body">
        <slot name="body"></slot>
      </div>
      <div class="modal-footer">
        <slot name="footer"></slot>
      </div>
    </div>
    <div class="backdrop"></div>
  </div>
</template>

<style scoped>
.modal-dialog {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.backdrop {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(48, 48, 48, 0.5);
  z-index: 10;
}

.modal {
  width: 70%;
  min-width: 350px;
  min-height: 40vh;
  background-color: white;
  border-radius: 12px;
  z-index: 100;
  box-sizing: border-box;
}

.modal-header {
  border-bottom: 1px solid #ddd;
  padding: 0 20px;
  box-sizing: border-box;
  background-color: #565656;
  padding: 15px 20px;
  border-top-left-radius: 12px;
  border-top-right-radius: 12px;
  color: white;
  font-family: 'Space Grotesk', sans-serif;
}

.modal-body {
  padding: 20px;
  box-sizing: border-box;
  font-family: 'Space Grotesk', sans-serif;
}
</style>
