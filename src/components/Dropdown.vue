<template>
  <div class="dropdown">
    <div class="dropdown-input">
      <input
          placeholder="select todo to do"
          list="list-item"
          @keyup="filterArr"
          v-model="inputValue"
      >
    </div>
    <div class="dropdown-actions">
      <button class="input-clear" @click="clearInput">
        <img src="../assets/icons/clear.svg">
      </button>
    </div>
    <datalist id="list-item">
      <option
          v-for="item in inputValue.length > 0 ? filteredList : optionList" key="item.id"
      >{{ item.title }}</option>
    </datalist>
  </div>
</template>

<script>
export default {
  name: "Dropdown",
  data() {
    return {
      optionList: [],
      inputValue: '',
      filteredList: [],
      isListVisible: false
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/photos')
        .then(response => response.json())
        .then(json => this.optionList =
            json.reduce((reducer, option) => [...reducer, option, {...option, ...{title: option.title+1}}], []))
  },
  methods: {
    filterArr() {
      this.filteredList = this.optionList.filter(item => item.title.toLowerCase().includes(this.inputValue.toLowerCase()))
    },
    clearInput() {
      this.inputValue = '';
    }
  }
}
</script>

<style lang="scss" scoped>
.dropdown {
  margin-top: 100px;
  display: flex;
  border: 1px solid rgba(105, 105, 105, 0.48);
  border-radius: 5px;
  padding: 10px;

  &-actions {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 35px;

    button {
      height: 35px;
      border: none;
      cursor: pointer;
      background: transparent;
    }
  }

  input {
    width: 400px;
    height: 35px;
    font-size: 20px;
    border: none;
    outline: none;
    flex-shrink: 1;

    &::-webkit-calendar-picker-indicator {
      display: none !important;
    }
  }
  ul {
    li {
      cursor: pointer;
      border: 1px solid gray;
    }
  }
}
</style>