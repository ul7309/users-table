<template>
  <button
    :type="type"
    class="btn"
    @click="onClick"
    :disabled="disabled"
  >
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'UiButton',
  props: {
    type: {
      type: String,
      default: 'button',
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    onClick() {
      this.$emit('on-click');
    },
  },
};
</script>

<style scoped lang="scss">
.btn {
  border-radius: 2px;
  border: 0;
  background-color: #4468ca;
  color: #fff;
  padding: 5px 10px;
  cursor: pointer;
  transition: all .3s;

  &:hover {
    opacity: .8;
  }

  &:disabled {
    opacity: .5;
    cursor: auto;
  }
}
</style>