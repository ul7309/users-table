<template>
  <div id="app">
    <UiButton @click.native="toggleModal">Добавить</UiButton>

    <UiTable
      :headers="tableHeaders"
      :body="users"
    />

    <UiModal
      v-if="isModalVisible"
      title="Добавить пользователя"
      @close-modal="toggleModal"
    >
      <Form
        @add-user="addUser"
        :users="users"
      />
    </UiModal>
  </div>
</template>

<script>
import UiButton from "@/components/ui/ui-button/Button";
import UiModal from "@/components/ui/ui-modal/Modal";
import UiTable from "@/components/ui/ui-table/Table";

import Form from "@/components/Form";

export default {
  name: "App",
  components: {
    UiButton,
    UiModal,
    UiTable,
    Form,
  },
  data() {
    return {
      tableHeaders: [
        {
          title: 'Имя',
        },
        {
          title: 'Телефон',
        }
      ],
      users: [
        {
          name: 'Марина',
          phone: '3',
        },
        {
          name: 'Петр',
          phone: '1',
        },
      ],
      isModalVisible: false,
    };
  },
  methods: {
    toggleModal() {
      this.isModalVisible = !this.isModalVisible;
    },
    addUser(value) {
      let $this = this;

      let getProp = (obj) => {
        for (let prop in obj) {
          if (typeof(obj[prop]) === 'object') {
            if (obj[prop].name === value.chief) {
              obj[prop].items
                ? obj[prop].items.push(value)
                : $this.$set(obj[prop], 'items', [value]);
            } else {
              getProp(obj[prop]);
            }
          }
        }
      }

      if (value.chief) {
        getProp(this.users);
      } else {
        this.users.push(value);
      }

      this.saveUsersStorage();
      this.toggleModal();
    },
    saveUsersStorage() {
      localStorage.setItem('users', JSON.stringify(this.users));
    },
    getUsersStorage() {
      this.users = JSON.parse(localStorage.getItem('users'));
    },
  },
  mounted() {
    localStorage.getItem('users') ? this.getUsersStorage() : this.saveUsersStorage();
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  max-width: 500px;
  margin: 0 auto;
}
</style>
