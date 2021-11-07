<template>
  <form class="form">
    <div>{{ surname }}</div>
    <h3>Личные данные</h3>
    <section class="lineGroup">
      <div class="inputWrapper">
        <label for="surname" class="label">Фамилия</label>
        <a-input
          id="surname"
          placeholder="Фамилия"
          size="large"
          v-model="surname"
        />
      </div>

      <div class="inputWrapper">
        <label for="name" class="label">Имя</label>
        <a-input id="name" placeholder="Имя" size="large" v-model="name" />
      </div>

      <div class="inputWrapper">
        <label for="middleName" class="label">Отчество</label>
        <a-input
          id="middleName"
          placeholder="Отчество"
          size="large"
          v-model="middleName"
        />
      </div>
    </section>
  </form>
</template>

<script>
import Input from "ant-design-vue/lib/input";
import "ant-design-vue/lib/input/style/index.css";

export default {
  data() {
    return {
      surname: "",
      name: "",
      middleName: "",
    };
  },
  components: {
    "a-input": Input,
  },
  methods: {},
};
</script>

<style scoped>
.label {
  display: block;
  padding: 6px 0;
  font-size: 16px;
  color: grey;
}

.inputWrapper {
  width: 30%;
  margin-right: 10px;
}

.lineGroup {
  display: flex;
}

.form {
}
</style>
