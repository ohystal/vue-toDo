<script setup>
import { ref } from 'vue';

const emit = defineEmits(["onSubmit"]);

const title = ref('')

const onSubmit = () => {
  emit("onSubmit", {
    id: Math.round(Math.random() * 30),
    title: title.value,
  });
  title.value = "";
};
</script>

<template>
  <form class="flex m-auto gap-2.5" @submit.prevent="onSubmit">
    <input
      v-model="title"
      class="rounded p-3"
      type="text"
      required
      placeholder="Enter task"
    />
    <button type="submit">Add Task</button>
  </form>
</template>
