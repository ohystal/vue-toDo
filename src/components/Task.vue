<script setup>
const props = defineProps({
  item: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(["remove", "complete"]);

const handleRemove = () => {
  emit("remove", { ...props.item });
};

const handleComplete = () => {
  emit('complete', { 
    item: props.item,
    completed: event.target.checked 
  });
};
</script>

<template>
  <div
    class="flex gap-2 mb-5 rounded-md items-center border-2 border-dashed border-orange-600 justify-between"
  >
    <input class="w-8" type="checkbox" @change="handleComplete" />
    <p>{{ item.title }}</p>
    <button class="font-bold" type="button" @click="handleRemove">
      Remove
    </button>
  </div>
</template>

<style scoped>
button {
  padding: 10px;
  background: none;
}
button:hover {
  background: #b34949;
}
</style>
