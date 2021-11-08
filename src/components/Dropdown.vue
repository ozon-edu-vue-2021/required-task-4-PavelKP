<template>
  <div v-click-outside="handleClickOutside" class="wrapper">
    <input
      @focus="isOpened = true"
      @input="throttledSearch($event.target.value)"
      @keyup.enter="handleClickOutside"
      type="search"
      class="input"
      :value="value"
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
import { throttle } from "../utils";
export default {
  data() {
    return {
      isOpened: false,
      filteredData: [],
      throttledSearch: null,
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
    handleClickOutside() {
      console.log("click outside");
      const value = this.$props.value;

      if (this.isOpened) {
        this.isOpened = false;
        const fullMatch = this.$props.data.find((item) => {
          return item?.[this.fieldName]?.toLowerCase() === value?.toLowerCase();
        })?.[this.fieldName];

        if (fullMatch) {
          this.$emit("input", fullMatch);
        } else {
          this.$emit("input", "");
        }

        this.filteredData = [...this.$props.data];
      }
    },
    hideDropdown() {
      this.isOpened = false;
    },
    handleClick(item) {
      this.hideDropdown();
      this.$emit("input", item[this.fieldName]);
    },
    handleInput(item) {
      if (!this.isOpened) {
        this.isOpened = true;
      }

      this.$emit("input", item);
      const regExp = new RegExp(`${item}`, "i");
      const filteredData = this.$props.data.filter((item) =>
        regExp.test(item?.[this.fieldName])
      );

      this.filteredData = [...filteredData];
    },
  },
  created() {
    this.filteredData = [...this.$props.data];
    this.throttledSearch = throttle(this.handleInput, 1000);
  },
  updated() {
    console.log("updated");
  },
};
</script>

<style scoped>
.wrapper {
  position: relative;
  width: 300px;
}

.input {
  width: 100%;
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
