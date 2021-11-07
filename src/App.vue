<template>
  <div id="app">
    <Form :citizenships="citizenships" :passportTypes="passportTypes" />
  </div>
</template>

<script>
import Form from "./components/Form.vue";
import citizenships from "@/assets/data/citizenships.json";
import passportTypes from "@/assets/data/passport-types.json";

export default {
  name: "App",
  components: {
    Form,
  },
  data() {
    return {
      citizenships: null,
      passportTypes: null,
    };
  },
  created() {
    this.citizenships = citizenships;
    this.passportTypes = passportTypes;
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  background-color: #fafafa;
  padding: 24px;
  box-sizing: border-box;
}

html,
body,
#app {
  height: 100%;
}

* {
  box-sizing: border-box;
}
</style>
