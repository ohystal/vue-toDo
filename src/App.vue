<script setup>
import Task from "./components/Task.vue";
import Form from "./components/Form.vue";
import { reactive } from "vue";

const todos = reactive([]);
const completed = reactive([]);

const handleSubmit = (item) => todos.push(item);

const removeItem = (item) => {
  const index = todos.findIndex((todo) => todo.id === item.id);
  if (index !== -1) {
    todos.splice(index, 1);
  }
};

const completeTask = ({ item, completed: isCompleted }) => {
  const sourceArray = isCompleted ? todos : completed;
  const targetArray = isCompleted ? completed : todos;
  
  const index = sourceArray.findIndex(i => i.id === item.id);
  if (index !== -1) {
    const [movedItem] = sourceArray.splice(index, 1);
    targetArray.push(movedItem);
  }
};
</script>

<template>
  <div class="flex flex-col h-[300px]">
    <h2 class="text-3xl font-bold 3 underline mb-2 text-left">ToDo</h2>
    <ul class="my-auto max-h-[300px] overflow-y-scroll">
      <li class="max-h-full" v-for="item in todos" :key="item.id">
        <Task :item="item" :title="item.title" @remove="removeItem" @complete="completeTask"/>
      </li>
    </ul>
  </div>
  <Form @onSubmit="handleSubmit" />
  <div class="flex flex-col h-[300px]">
    <ul class="my-auto max-h-[300px] overflow-y-scroll">
      <li class="max-h-full" v-for="item in completed" :key="item.id">
        <Task :item="item" :title="item.title" @remove="removeItem" @complete="completeTask"/>
      </li>
    </ul>
    <h2 class="text-3xl font-bold underline mb-2 text-right">Complete</h2>
  </div>
</template>
