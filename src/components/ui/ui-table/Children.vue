<template>
  <div class="table__nested">
    <div class="table__row">
      <div class="table__cell">{{ children.name }}</div>

      <div class="table__cell">{{ children.phone }}</div>
    </div>

    <Children
      v-for="(child, index) in children.items"
      :key="index"
      :children="child"
    />
  </div>
</template>

<script>
export default {
  name: "Children",
  props: {
    children: {
      type: Object,
      default: () => {},
    },
  },
};
</script>
