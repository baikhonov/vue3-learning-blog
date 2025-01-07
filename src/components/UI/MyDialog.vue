<template>
  <div class="dialog" v-if="show" @click="hideDialog">
    <div class="dialog__content" @click.stop>
      <button class="dialog__close-btn" @click="hideDialog"></button>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "my-dialog",
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    hideDialog() {
      this.$emit('update:show', false);
    }
  }
}
</script>

<style scoped>
.dialog {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;

  background-color: rgba(0, 0, 0, 0.5);
}

.dialog__close-btn {
  position: absolute;
  right: 8px;
  top: 5px;
  width: 30px;
  height: 30px;
  background-color: transparent;
  border: none;
  cursor: pointer;
}
.dialog__close-btn::before {
  content: '';
  position: absolute;
  right: 3px;
  top: 15px;
  width: 15px;
  height: 1px;
  background-color: #000;
  transform: rotate(45deg);
}
.dialog__close-btn::after {
  content: '';
  position: absolute;
  right: 3px;
  top: 15px;
  width: 15px;
  height: 1px;
  background-color: #000;
  transform: rotate(135deg);
}

.dialog__content {
  position: relative;
  min-width: 350px;
  min-height: 50px;
  margin: auto;
  padding: 20px;

  background-color: white;
  border-radius: 12px;
}
</style>