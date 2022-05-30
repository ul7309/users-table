<template>
  <form class="form">
    <div class="form__row">
      <UiInput
        id="name"
        placeholder="Введите имя"
        label="Имя"
        @on-input="setName"
      />
    </div>

    <div class="form__row">
      <UiInput
        id="phone"
        placeholder="Введите телефон"
        label="Телефон"
        @on-input="setPhone"
      />
    </div>

    <div v-if="isUsers" class="form__row">
      <UiSelect
        placeholder="Выберите начальника"
        label="Начальник"
        :options="usersFormatted"
        @on-change="onChange"
      />
    </div>

    <div class="form__row">
      <UiButton
        :disabled="!isRequired"
        @on-click="addUser"
      >
        Сохранить
      </UiButton>
    </div>
  </form>
</template>

<script>
import UiInput from '@/components/ui/ui-input/Input.vue';
import UiButton from "@/components/ui/ui-button/Button";
import UiSelect from "@/components/ui/ui-select/Select";

export default {
  name: 'FormAddUser',
  props: {
    users: {
      type: Array,
      default: () => [],
    },
  },
  components: {
    UiInput,
    UiButton,
    UiSelect,
  },
  data() {
    return {
      form: {
        name: '',
        phone: '',
        chief: '',
      },
    };
  },
  computed: {
    isUsers() {
      return this.users.length > 0;
    },
    isRequired() {
      return this.form.name.length !== 0 && this.form.phone.length !== 0 ? true : false;
    },
    usersFormatted() {
      let users = [];

      let getProp = (obj) => {
        for (let prop in obj) {
          if (typeof(obj[prop]) === 'object') {
            getProp(obj[prop]);
          } else if (prop === 'name') {
            users.push({ name: obj[prop] });
          }
        }
      }

      getProp(this.users);

      return users;
    },
  },
  methods: {
    setName(value) {
      this.form.name = value;
    },
    setPhone(value) {
      this.form.phone = value;
    },
    onChange(value) {
      this.form.chief = value;
    },
    addUser() {
      if (!this.isRequired) return false;

      this.$emit('add-user', this.form);
    },
  },
};
</script>

<style scoped lang="scss">
.form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
</style>
