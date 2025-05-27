<script setup>
import Task from "./components/Task.vue";
import Form from "./components/Form.vue";
import { reactive, computed } from "vue";

const todos = reactive([]);

const handleSubmit = (item) => todos.push(item);

const removeItem = (item) => {
  const index = todos.findIndex((todo) => todo.id === item.id);

  if (index !== -1) {
    todos.splice(index, 1);
  }
};

const isChecked = ({ item, completed }) => {
  const todo = todos.find((todo) => todo.id === item.id);
  if (todo) {
    todo.completed = completed;
  }
};

const completeTasks = computed(() => {
  return todos.filter((item) => item.completed);
});

const pendingTasks = computed(() => {
  return todos.filter((item) => !item.completed);
});

const handleUpTask = ({item}) => {
  const index = todos.findIndex((todo)=>todo.id===item.id)

  if (index > 0) {
    [todos[index], todos[index - 1]] = [todos[index - 1], todos[index]];
  }
}

const handleDownTask =({item}) => {
  const index = todos.findIndex((todo)=>todo.id===item.id)

  if (index < todos.length - 1) {
    [todos[index], todos[index + 1]] = [todos[index + 1], todos[index]];
  }
}
</script>

<template>
  <div class="flex flex-col h-[300px]">
    <h2 class="text-3xl font-bold 3 underline mb-2 text-left">ToDo</h2>
    <ul class="my-auto max-h-[300px] overflow-y-scroll">
      <li class="max-h-full" v-for="(item, index) in pendingTasks" :key="item.id">
        <Task
          :item="item"
          :title="item.title"
          :isLast="index === pendingTasks.length - 1"
          :isFirst="index === 0"
          @remove="removeItem"
          @complete="isChecked"
          @upTask="handleUpTask"
          @downTask="handleDownTask"
        />
      </li>
    </ul>
  </div>
  <Form @onSubmit="handleSubmit" />
  <div class="flex flex-col h-[300px]">
    <ul class="my-auto max-h-[300px] overflow-y-scroll">
      <li class="max-h-full" v-for="(item, index) in completeTasks" :key="item.id">
        <Task
          :item="item"
          :title="item.title"
          :isLast="index === completeTasks.length - 1"
          :isFirst="index === 0"
          @remove="removeItem"
          @complete="isChecked"
          @upTask="handleUpTask"
          @downTask="handleDownTask"
        />
      </li>
    </ul>
    <h2 class="text-3xl font-bold underline mb-2 text-right">Complete</h2>
  </div>
</template>
