<template>
  <div v-click-outside="hideDropdown" class="wrapper">
    <input
      @focus="isOpened = true"
      type="text"
      class="input"
      :value="value"
      @input="handleInput($event.target.value)"
      :placeholder="placeholder"
    />
    <div v-if="isOpened">
      <ul class="list" v-if="filteredData.length">
        <li
          class="listItem"
          v-for="item in filteredData"
          :key="item.id"
          @click="handleClick(item)"
        >
          {{ item[fieldName] }}
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
      filteredData: [],
    };
  },
  directives: {
    ClickOutside,
  },
  props: {
    data: {
      type: Array,
      default: () => [],
    },
    value: String,
    fieldName: {
      type: String,
      require: true,
    },
    placeholder: String,
  },
  methods: {
    hideDropdown() {
      this.isOpened = false;
    },
    handleClick(item) {
      this.hideDropdown();
      this.$emit("input", item[this.fieldName]);
    },
    handleInput(item) {

			// trottling + foo + clear button
      this.$emit("input", item);
      const regExp = new RegExp(`${item}`, "i");
      const foo = this.$props.data.slice();
      const filteredData = foo.filter(({ nationality }) =>
        regExp.test(nationality)
      );
      this.filteredData.splice(0, this.filteredData.length);
      this.filteredData.push(...filteredData);
    },
  },
  created() {
    this.filteredData = [...this.$props.data];
  },
};
</script>

<style scoped>
.wrapper {
  position: relative;
}

.input {
  width: 300px;
  height: 40px;
  padding-left: 5px;
  border: 1px solid #d9d9d9;
  font-size: 16px;
}

.input::placeholder {
  color: #bfbfbf;
  font-size: 16px;
  line-height: 1.5;
}

.list {
  position: absolute;
  left: 0;
  top: 40px;
  width: 100%;
  padding: 0;
  margin: 0;
  z-index: 2;
  background-color: #ffffff;
  box-shadow: 0 2px 8px rgb(0 0 0 / 15%);
  max-height: calc(40px * 5);
  list-style: none;
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
  cursor: pointer;
}

.listItem:hover {
  background-color: #1890ff;
  color: #ffffff;
}
</style>
