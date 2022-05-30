<template>
  <div class="table">
    <div class="table__header">
      <div
        v-for="(item, index) in headers"
        :key="index"
        class="table__cell"
        @click="sortBody($event.target.innerText)"
      >
      {{ item.title }}
      </div>
    </div>

    <div v-if="isBody" class="table__body">
      <div
        v-for="(item, bodyIndex) in localBody"
        :key="bodyIndex"
        class="table__row"
      >
        <div class="table__cell">{{ item.name }}</div>

        <div class="table__cell">{{ item.phone }}</div>

        <Children
          v-for="(children, childrenIndex) in item.items"
          :key="childrenIndex"
          :children="children"
        />
      </div>
    </div>
    <div v-else class="table__empty">Данных не найдено</div>
  </div>
</template>

<script>
import Children from './Children.vue';
export default {
  name: "UiTable",
  components: {
    Children,
  },
  props: {
    headers: {
      type: Array,
      default: () => [],
    },
    body: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      localBody: this.body,
    };
  },
  computed: {
    isBody() {
      return this.body.length > 0;
    },
  },
  methods: {
    sortByName(array) {
      array.sort((a, b) => a.name > b.name ? 1 : -1);
    },
    sortByPhone(array) {
      array.sort((a, b) => a.phone - b.phone);
    },
    sorting(value, array) {
      value === 'Имя' ? this.sortByName(array) : this.sortByPhone(array);
    },
    sortBody(value) {
      let $this = this;

      let getProp = (obj) => {
        for (let prop in obj) {
          if (typeof(obj[prop]) === 'object') {
            getProp(obj[prop]);

            if (Array.isArray(obj[prop])) $this.sorting(value, obj[prop]);
          } else {
            $this.sorting(value, $this.localBody);
          }
        }
      }

      getProp(this.localBody);
    }
  },
  updated() {
    this.localBody = this.body;
  },
};
</script>

<style scoped lang="scss">
.table {
  margin-top: 10px;
  border: 1px solid #ededed;
  border-bottom: 0;
  border-radius: 5px;

  &__header {
    display: flex;
    cursor: pointer;
  }

  &__row {
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    border-top: 1px solid #ededed;
    margin-top: -1px;
  }

  &__cell {
    width: 50%;
    padding: 10px;
    text-align: left;
    box-sizing: border-box;
    border-bottom: 1px solid #ededed;

    &:first-child {
      border-right: 1px solid #ededed;
    }
  }

  &__empty {
    text-align: center;
    padding: 10px;
    border-top: 1px solid #ededed;
  }

  &__nested::v-deep {
    width: 100%;
    margin-left: 20px;

    .table__row {
      display: flex;
      flex-wrap: wrap;
      border-top: 1px solid #ededed;
      border-left: 1px solid #ededed;
      margin-top: -1px;

      .table__cell {
        padding: 10px;
        box-sizing: border-box;

        &:nth-child(1) {
          flex: 1;
          border-right: 1px solid #ededed;
              border-bottom: 1px solid #ededed;
        }

        &:nth-child(2) {
          width: 249px;
          flex: 0 0 249px;
        }
      }

      & + .table__nested {
        margin-left: 20px;
      }
    }
  }
}
</style>
