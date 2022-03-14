<template>
  <div id="app"></div>
  <mainHeader></mainHeader>
  <mainInput @addInput="addTodo"></mainInput>
  <mainList v-bind:listItems="todoItems" @removeList="removeTodo"></mainList>
  <mainFooter @removeAll="clearAll"></mainFooter>
</template>

<script>
import MainHeader from "@/components/MainHeader.vue";
import MainInput from "@/components/MainInput.vue";
import MainList from "@/components/MainList.vue";
import MainFooter from "@/components/MainFooter.vue";

export default {
  name: 'App',
  data() {
    return {
      todoStorage: localStorage,//#reference: test > sessionStorage
      todoItems: [],
      todoName: 'mapTodo'
    }
  },
  created() {
    if (this.todoStorage.length <= 0 || null === JSON.parse(this.todoStorage.getItem(this.todoName))) {
      return;
    }

    let mapTodo = JSON.parse(this.todoStorage.getItem('mapTodo'));
    let items = this.todoItems;
    Object.keys(mapTodo).sort().forEach(function(key){
      let value = mapTodo[key];
      items.push({key, value});
    });
  },
  methods: {
    initializeMap(key) {
      if (this.todoStorage.length > 0 && null != JSON.parse(this.todoStorage.getItem(this.todoName))) {
        return;
      }
      this.todoStorage.setItem(key, JSON.stringify({}));
    },
    addTodo(key, value) {
      this.initializeMap(this.todoName);
      let mapTodo = JSON.parse(this.todoStorage.getItem(this.todoName));
      mapTodo[key] = value;
      this.todoStorage.setItem(this.todoName, JSON.stringify(mapTodo));
      this.todoItems.push({key, value});
    },
    removeTodo(key, index) {
      console.log(key, index);
      let mapTodo = JSON.parse(this.todoStorage.getItem(this.todoName));
      delete mapTodo[key];
      this.todoStorage.setItem(this.todoName, JSON.stringify(mapTodo));
      this.todoItems.splice(index, 1);
      //this.todoItems.splice(this.todoItems.findIndex(element => element.key == key), 1);
    },
    clearAll() {
      this.todoStorage.removeItem(this.todoName);
      this.todoItems = [];
    }
  },
  components: {
    'mainHeader': MainHeader,
    'mainInput': MainInput,
    'mainList': MainList,
    'mainFooter': MainFooter
  }
}
</script>

<style>
  body {
    text-align: center;
    background-color: #F6F6F8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
</style>
