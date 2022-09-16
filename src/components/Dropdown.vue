<template>
  <div class="dropdown">
    <input placeholder="select todo to do" list="list-item" @keyup="filterArr" v-model="inputValue">
    <datalist id="list-item">
      <option v-for="item in inputValue.length > 0 ? filteredList : optionList" key="item.id">{{ item.title }}</option>
    </datalist>
  </div>
</template>

<script>
export default {
  name: "Dropdown",
  data(){
    return {
      optionList: [],
      inputValue: '',
      filteredList: []
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos')
        .then(response => response.json())
        .then(json => this.saveData(json))
  },
  methods:{
    saveData(data){
      this.optionList = data;
    },
    filterArr(){
      this.filteredList = this.optionList.filter(item => item.title.toLowerCase().includes(this.inputValue.toLowerCase()))
    }
  }
}
</script>

<style lang="scss" scoped>
.dropdown {
  margin-top: 100px;
  input {
    width: 400px;
    height: 35px;
    padding: 10px;
    font-size: 20px;
    border-radius: 5px;
    border: 1px solid rgba(105, 105, 105, 0.48);
    &:focus-visible {
      border: none
    }
  }
  datalist {
    position: absolute;
    background-color: white;
    border: 1px solid blue;
    border-radius: 0 0 5px 5px;
    border-top: none;
    font-family: sans-serif;
    width: 350px;
    padding: 5px;
    max-height: 10rem;
    overflow-y: auto;
    option {
      background-color: white;
    }
  }

  option:hover,  .active{
    background-color: lightblue;
  }
}
</style>