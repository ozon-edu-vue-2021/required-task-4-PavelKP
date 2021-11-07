<template>
  <div v-click-outside="hideDropdown">
    <input @focus="isOpened = true" type="text" name="" class="input" />
    <div v-if="isOpened">
      <ul class="list" v-if="data.length">
        <li class="listItem" v-for="item in data" :key="item.id">
          {{ item.nationality }}
        </li>
      </ul>
      <ul v-else class="list empty">
        <li class="listItem">Ничего не найдено</li>
      </ul>
    </div>
  </div>
</template>

<script>
import ClickOutside from "vue-click-outside";

export default {
  data() {
    return {
      isOpened: false,
    };
  },
  directives: {
    ClickOutside,
  },
  props: {
    data: Array,
  },
  methods: {
    hideDropdown() {
      this.isOpened = false;
    },
  },
};
</script>

<style scoped>
.input {
  width: 300px;
  height: 40px;
  font-size: 16px;
}

.list {
  list-style: none;
  padding: 0;
  margin: 0;
  background-color: #ffffff;
  box-shadow: 0 2px 8px rgb(0 0 0 / 15%);
  max-height: calc(40px * 5);
  overflow-x: hidden;
  overflow-y: scroll;
}

.empty {
  overflow: hidden;
}

.listItem {
  height: 40px;
  padding: 10px 5px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}
</style>
