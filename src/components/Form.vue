<template>
  <form class="form">
    <div>{{ formData.citizenship }}</div>
    <h3 class="header">Личные данные</h3>
    <section class="lineGroup">
      <div class="inputWrapper">
        <label for="surname" class="label text">Фамилия</label>
        <a-input
          id="surname"
          placeholder="Фамилия"
          size="large"
          v-model="formData.surname"
        />
      </div>

      <div class="inputWrapper">
        <label for="name" class="label text">Имя</label>
        <a-input
          id="name"
          placeholder="Имя"
          size="large"
          v-model="formData.name"
        />
      </div>

      <div class="inputWrapper">
        <label for="middleName" class="label text">Отчество</label>
        <a-input
          id="middleName"
          placeholder="Отчество"
          size="large"
          v-model="formData.middleName"
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
          v-model="formData.birthDate"
        />
      </div>
    </section>

    <section class="lineGroup">
      <div class="inputWrapper">
        <label for="email" class="label text">E-mail</label>
        <a-input
          id="email"
          placeholder="Введите e-mail"
          size="large"
          v-model="formData.email"
        />
      </div>
    </section>

    <h3 class="header">Пол</h3>
    <section class="lineGroup">
      <a-radio-group v-model="formData.gender" size="large">
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
        <label class="label text">Гражданство</label>
        <c-dropdown
          :data="citizenships"
          v-model="formData.citizenship"
          fieldName="nationality"
        />
      </div>
    </section>
    <section class="lineGroup" v-if="formData.citizenship === 'Russia'">
      <div class="inputWrapper">
        <label for="passportSeries" class="label text">Серия паспорта</label>
        <a-input
          id="passportSeries"
          placeholder="Введите серию"
          size="large"
          v-model="formData.passportSeries"
        />
      </div>

      <div class="inputWrapper">
        <label for="passportNumber" class="label text">Номер паспорта</label>
        <a-input
          id="passportNumber"
          placeholder="Введите номер"
          size="large"
          v-model="formData.passportNumber"
        />
      </div>

      <div class="inputWrapper">
        <label for="passportDate" class="label text">Дата выдачи</label>
        <a-input
          id="passportDate"
          placeholder="Введите дату выдачи"
          size="large"
          v-model="formData.passportDate"
        />
      </div>
    </section>
    <div v-else>
      <section class="lineGroup">
        <div class="inputWrapper">
          <label for="latinName" class="label text">Имя на латинице</label>
          <a-input
            id="latinName"
            placeholder="Введите имя"
            size="large"
            v-model="formData.latinName"
          />
        </div>
        <div class="inputWrapper">
          <label for="latinSurname" class="label text"
            >Фамилия на латинице</label
          >
          <a-input
            id="latinSurname"
            placeholder="Введите фамилию"
            size="large"
            v-model="formData.latinSurname"
          />
        </div>
      </section>
      <p class="tip">
        Иностраницы заполняют латинскими буквами. Например, ivanov ivan
      </p>
      <section class="lineGroup">
        <div class="inputWrapper">
          <label for="passportNumber" class="label text">Номер паспорта</label>
          <a-input
            id="passportNumber"
            placeholder="Введите номер"
            size="large"
            v-model="formData.passportNumber"
          />
        </div>
        <div class="inputWrapper">
          <label class="label text">Страна выдачи</label>
          <c-dropdown
            :data="citizenships"
            v-model="formData.passportCountry"
            fieldName="nationality"
            placeholder="Выберите страну выдачи"
          />
        </div>
        <div class="inputWrapper">
          <label class="label text">Тип паспорта</label>
          <c-dropdown
            :data="passportTypes"
            v-model="formData.passportType"
            fieldName="type"
            placeholder="Выберите тип паспорта"
          />
        </div>
      </section>
    </div>

    <h3 class="header">Меняли ли фамилию или имя?</h3>
    <section class="lineGroup">
      <a-radio-group v-model="formData.isChanged" size="large">
        <a-radio value="true">
          <span class="text">Да</span>
        </a-radio>
        <a-radio value="false">
          <span class="text">нет</span>
        </a-radio>
      </a-radio-group>
    </section>

    <section class="lineGroup" v-if="formData.isChanged === 'true'">
      <div class="inputWrapper">
        <label for="prevSurname" class="label text">Предыдущая фамилия</label>
        <a-input
          id="prevSurname"
          placeholder="Введите фамилию"
          size="large"
          v-model="formData.prevSurname"
        />
      </div>
      <div class="inputWrapper">
        <label for="prevName" class="label text">Предыдущее имя</label>
        <a-input
          id="prevName"
          placeholder="Введите имя"
          size="large"
          v-model="formData.prevName"
        />
      </div>
    </section>
    <div class="buttonWrapper">
      <a-button type="primary" size="large" @click="handleFormSubmit"
        >Отправить</a-button
      >
    </div>
  </form>
</template>

<script>
import Input from "ant-design-vue/lib/input";
import Radio from "ant-design-vue/lib/radio";
import Button from "ant-design-vue/lib/button/button";
import CustomDropdown from "./Dropdown.vue";
import "ant-design-vue/lib/input/style/index.css";
import "ant-design-vue/lib/radio/style/index.css";
import "ant-design-vue/lib/button/style/index.css";

export default {
  data() {
    return {
      formData: {
        surname: "",
        name: "",
        middleName: "",
        birthDate: "",
        email: "",
        gender: "male",
        citizenship: "Russia",
        passportSeries: "",
        passportDate: "",
        passportNumber: "",
        latinName: "",
        latinSurname: "",
        passportCountry: "",
        passportType: "",
        isChanged: "false",
        prevName: "",
        prevSurname: "",
      },
    };
  },
  props: {
    citizenships: Array,
    passportTypes: Array,
  },
  components: {
    "a-input": Input,
    "a-radio": Radio,
    "a-radio-group": Radio.Group,
    "a-button": Button,
    "c-dropdown": CustomDropdown,
  },
  methods: {
    handleFormSubmit() {
      const clearedData = { ...this.formData };
      for (let key in clearedData) {
        if (!clearedData[key]) {
          delete clearedData[key];
        }
      }
      console.log(clearedData);
    },
  },
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

.tip {
  padding: 0;
  margin: 0;
  margin-bottom: 15px;
  font-size: 14px;
  color: rgb(182, 180, 180);
}

.buttonWrapper {
  padding: 20px 0;
  max-width: 1000px;
}

.form {
}
</style>
