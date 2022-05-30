<template>
  <label :for="id">
    <span class="label">{{ label }}</span>

    <input
      :type="type"
      :id="id"
      :placeholder="placeholder"
      class="input"
      @input="onInput"
    >
  </label>
</template>

<script>
export default {
  name: 'UiInput',
  props: {
    type: {
      type: String,
      default: 'text',
    },
    label: {
      type: String,
      default: '',
    },
    placeholder: {
      type: String,
      default: '',
    },
    id: {
      type: String,
      default: '',
    },
  },
  methods: {
    onInput(event) {
      this.$emit('on-input', event.target.value);
    },
  },
};
</script>

<style scoped lang="scss">
.label {
  min-width: 100px;
  display: inline-block;
  font-size: 14px;
}
</style>