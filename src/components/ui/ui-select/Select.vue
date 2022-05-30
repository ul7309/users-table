<template>
  <div>
    <span class="label">{{ label }}</span>

    <select
      v-model="selected"
      @change="onChange($event)"
    >
      <option
        v-if="placeholder"
        disabled
        value=""
      >
        {{ placeholder }}
      </option>

      <option
        v-for="(option, index) in options"
        :key="index"
        :value="option.name"
      >
        {{ option.name }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  props: {
    placeholder: {
      type: String,
      default: '',
    },
    label: {
      type: String,
      default: '',
    },
    options: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      selected: '',
    };
  },
  methods: {
    onChange() {
      this.$emit('on-change', this.selected);
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
