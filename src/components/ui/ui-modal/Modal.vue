<template>
  <div class="modal">
    <div class="modal__overlay" @click="closeModal"></div>

    <div class="modal__wrap">
      <button type="button" class="modal__close" @click="closeModal">x</button>

      <div class="modal__title">{{ title }}</div>

      <div class="modal__body">
        <slot></slot>
      </div>

      <div class="modal__footer">
        <slot name="footer"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'UiModal',
  props: {
    title: {
      type: String,
      default: '',
    },
  },
  methods: {
    closeModal() {
      this.$emit('close-modal');
    },
  },
};
</script>

<style scoped lang="scss">
.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;

  &__overlay {
    background-color: rgba(0, 0, 0, 0.3);
    width: 100%;
    height: 100%;
  }

  &__wrap {
    max-width: 300px;
    width: 100%;
    margin: auto;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 1;
    background: #fff;
    padding: 20px;
    border-radius: 5px;
  }

  &__close {
    background-color: transparent;
    border: 0;
    font-size: 22px;
    position: absolute;
    top: -5px;
    right: 0;
    cursor: pointer;
    padding: 10px;
    transition: all .3s;

    &:hover {
      opacity: .5;
    }
  }

  &__title {
    margin-bottom: 10px;
    font-size: 18px;
  }

   &__footer {
     margin-top: 20px;
   }
}
</style>