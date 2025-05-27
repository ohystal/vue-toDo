<script setup>
const props = defineProps({
  item: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits(["remove", "complete", "upTask", "downTask"]);

const handleRemove = () => {
  emit("remove", { ...props.item });
};

const handleComplete = (event) => {
  emit("complete", {
    item: props.item,
    completed: event.target.checked,
  });
};

const handleUp = () => {
  emit("upTask", {
    item: props.item,
  });
};

const handleDown = () => {
  emit("downTask", {
    item: props.item,
  });
};
</script>

<template>
  <div
    class="flex gap-2 mb-5 rounded-md items-center border-2 border-dashed border-orange-600 justify-between"
  >
    <div>
      <input
        class="w-8"
        type="checkbox"
        :checked="item.completed"
        @change="handleComplete"
      />
      <button @click="handleUp">
        <img
          src="../assets/arrow.png"
          alt="стрелка вверх"
          width="20px"
          height="20px"
        />
      </button>
      <button @click="handleDown">
        <img
          class="rotate-[-180deg]"
          src="../assets/arrow.png"
          alt="стрелка вниз"
          width="20px"
          height="20px"
        />
      </button>
    </div>
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
