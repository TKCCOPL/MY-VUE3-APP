<script setup>
import mybutton from "./components/button.vue";
import { ref } from "vue";
import axios from "axios";

function adds(str1) {
  console.log(str1);
} 

getlist();

const value = ref("");
const list = ref([]);


async function getlist() {
  const res = await axios({
    url: "http://q6zv39.laf.run/get_list",
    method: "get"
  });

  list.value = res.data.list;
}

async function add() {
 await axios({
    url: "http://q6zv39.laf.run/add-todo",
    method: "post",
    data: {
      value: value.value,
      done: false,
    },
  });
  value.value = "";
  getlist();
}

async function update(id) {
  await axios({
    url: "http://q6zv39.laf.run/update_todo",
    method: "post",
    data: {
      id,
    },
  });
  // getlist();
}
async function del(id) {
  await axios({
    url: "http://q6zv39.laf.run/del_todo",
    method: "post",
    data: {
      id: id,
    },
  });
  getlist();
}
</script>

<template>
  <div class="app-container">
    <div class="title">Long的Todo App</div>
    <p>制作人:longjunrong</p>
    <div class="todo-form">
      <input
        v-model="value"
        type="text"
        @keyup.enter="add"
        class="todo-input"
        placeholder="Add a todo"
      />
      <div @click="add" class="to-button">
        <span>add todo</span>
      </div>
    </div>

    <div class="todo-list">
      <div
        v-for="(item, index) in list"
        class="item"
        :class="[item.done ? 'completed' : 'item']"
      >
        <div class="item-content">
          <input 
            @click="update(item._id)"
            v-model="item.done" 
            type="checkbox" 
          />
          <span class="name">
            {{ item.value }}
          </span>
          <mybutton @ok="adds" text="点我" />
          <div @click="del(item._id)" class="del">删除</div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 50px;
  background-color: #ffffff;
  border-radius: 10px;
  box-sizing: border-box;
}

.title {
  font-size: 30px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 20px;
}

.todo-form {
  display: flex;
  justify-content: center;
  width: 100%;
  margin-bottom: 20px;
}

.todo-input {
  padding-left: 15px;
  border: 1px solid #dfe1e5;
  outline: none;
  width: 60%;
  height: 50px;
  border-radius: 20px 0 0 20px;
}

.to-button {
  width: 100px;
  height: 52px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #ff416c;
  color: white;
  cursor: pointer;
  border-radius: 0 20px 20px 0;
}

.todo-list {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.completed {
  text-decoration: line-through;
  opacity: 0.4;
}

.del {
  color: #ff416c;
  cursor: pointer;
  user-select: none;
  margin-left: 10px;
}

.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 10px;
  box-sizing: border-box;
  margin: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 80%;
}

.item-content {
  display: flex;
  align-items: center;
  width: 100%;
}

.name {
  flex-grow: 1;
  margin-left: 10px;
}
</style>
