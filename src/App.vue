<!-- js  -->
<script setup>
import { ref } from 'vue';

const inputValue = ref('');
const todoList = ref([
  { key: '1', text: 'vue1', done: false },
  { key: '2', text: 'vue2', done: false },
  { key: '3', text: 'vue3', done: false },
  { key: '4', text: 'vue4', done: false },
  { key: '5', text: 'vue5', done: false },
  { key: '6', text: 'vue6', done: false },
]);

console.log(todoList.value);

const handleClickButton = () => {
  todoList.value.push({ key: '', text: inputValue.value, done: false });
};

const handleChange = (event) => {
  const nextValue = event.target.value;
  inputValue.value = nextValue;
};

const handleClickPop = (index) => {
  const choiceValue = '';
  //todoList.value.splice(index, 1);
  if (todoList.value[index - 1].done == true) {
    todoList.value.splice(index - 1, 1);
  }
};

const handleCheck = (key) => {
  console.log(key);
  if (todoList.value[key - 1].done == false)
    todoList.value[key - 1].done = true;
  else todoList.value[key - 1].done = false;
};

const items = ref([{ message: 'Foo' }, { message: 'Bar' }]);
</script>

<!-- html -->
<template>
  <h4>TODO LIST</h4>

  <input v-model="inputValue" />
  <button @click="handleClickButton">확인</button>
  <!-- <input :value="inputValue" @change="handleChange" /> -->

  <p>{{ todoList }}</p>
  <div class="todo-item" v-for="(item, index) in todoList">
    <input type="checkbox" @click="handleCheck(item.key)" v-model="item.done" />
    <span v-class="{ 'done-item': item.done }">{{ item.text }}</span>
    {{ item.key }} : {{ item.text }}
    <button @click="handleClickPop(item.key)">삭제</button>
  </div>
</template>

<!-- css -->
<style scoped>
.todo-item {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  border: 1px solid gray;
}
.done-item {
}
</style>
