<template>
  <form class="form">
    <div>{{ citizenship }}</div>
    <h3 class="header">Личные данные</h3>
    <section class="lineGroup">
      <div class="inputWrapper">
        <label for="surname" class="label text">Фамилия</label>
        <a-input
          id="surname"
          placeholder="Фамилия"
          size="large"
          v-model="surname"
        />
      </div>

      <div class="inputWrapper">
        <label for="name" class="label text">Имя</label>
        <a-input id="name" placeholder="Имя" size="large" v-model="name" />
      </div>

      <div class="inputWrapper">
        <label for="middleName" class="label text">Отчество</label>
        <a-input
          id="middleName"
          placeholder="Отчество"
          size="large"
          v-model="middleName"
        />
      </div>
    </section>

    <section class="lineGroup">
      <div class="inputWrapper">
        <label for="birthDate" class="label text">Дата рождения</label>
        <a-input
          id="birthDate"
          placeholder="Дата рождения"
          size="large"
          v-model="birthDate"
        />
      </div>
    </section>

    <section class="lineGroup">
      <div class="inputWrapper">
        <label for="email" class="label text">E-mail</label>
        <a-input
          id="email"
          placeholder="Дата рождения"
          size="large"
          v-model="email"
        />
      </div>
    </section>

    <h3 class="header">Пол</h3>
    <section class="lineGroup">
      <a-radio-group v-model="gender" size="large">
        <a-radio value="male">
          <span class="text">Мужской</span>
        </a-radio>
        <a-radio value="female">
          <span class="text">Женский</span>
        </a-radio>
      </a-radio-group>
    </section>

    <h3 class="header">Паспортные данные</h3>
    <section class="lineGroup">
      <div class="inputWrapper">
        <label for="birthDate" class="label text">Гражданство</label>
        <c-dropdown :data="citizenships" v-model="citizenship" />
      </div>
    </section>
  </form>
</template>

<script>
import Input from "ant-design-vue/lib/input";
import Radio from "ant-design-vue/lib/radio";
import CustomDropdown from "./Dropdown.vue";
import "ant-design-vue/lib/input/style/index.css";
import "ant-design-vue/lib/radio/style/index.css";

export default {
  data() {
    return {
      surname: "",
      name: "",
      middleName: "",
      birthDate: "",
      email: "",
      gender: "male",
      citizenship: "",
    };
  },
  props: {
    citizenships: Array,
  },
  components: {
    "a-input": Input,
    "a-radio": Radio,
    "a-radio-group": Radio.Group,
    "c-dropdown": CustomDropdown,
  },
  methods: {},
};
</script>

<style scoped>
.header {
  margin: 0;
  padding: 15px 0;
  font-size: 16px;
  color: black;
}

.text {
  font-size: 16px;
  color: grey;
}

.label {
  display: block;
  padding: 6px 0;
}

.inputWrapper {
  width: 30%;
  margin-right: 10px;
}

.lineGroup {
  display: flex;
  max-width: 1000px;
  margin-bottom: 10px;
}

.form {
}
</style>
