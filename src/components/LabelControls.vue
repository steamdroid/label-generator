<template>
  <section class="controls no-print mt-2">
    <div class="controls__tabs tabs mb-2">
      <button
        v-for="modeItem in modes"
        :key="modeItem.id"
        class="tabs__item"
        :class="{
          'tabs__item--active': modeItem.id === mode
        }"
        @click="handleModeChange(modeItem.id)"
        type="button"
      >
        {{ modeItem.title }}
      </button>
    </div>
    <input
      class="border-2 rounded-md px-2 mb-1"
      @input="handleTitleChange"
      type="text"
      name="title"
      placeholder="Название"
    />
    <input
      class="border-2 rounded-md px-2 mb-1"
      @input="handleDescriptionChange"
      type="text"
      name="desc"
      placeholder="Описание"
    />
    <input
      class="border-2 rounded-md px-2 mb-1"
      @input="handleImageSrcChange"
      type="text"
      name="imageSrcString"
      v-model="imageSrcString"
      :placeholder="mode === 'pic' ? 'Иконка' : 'Ссылка'"
    />
    <button
      type="button"
      class="border-2 rounded-md mt-3 px-3 py-2 text-white bg-cyan-800"
      @click="printLabel"
    >
      Напечатать
    </button>
  </section>
</template>
<script setup>
import { ref } from 'vue';
defineProps({
  mode: String
});

const modes = ref([
  {
    id: 'pic',
    title: 'Иконка'
  },
  {
    id: 'qr',
    title: 'QR-код'
  }
]);

const imageSrcString = ref('');

const emit = defineEmits(['setTitle', 'setDescription', 'setImageSrcString', 'setMode']);
const handleTitleChange = (e) => {
  emit('setTitle', e.target.value);
};
const handleDescriptionChange = (e) => {
  emit('setDescription', e.target.value);
};
const handleImageSrcChange = () => {
  emit('setImageSrcString', imageSrcString.value);
};
const handleModeChange = (newMode) => {
  imageSrcString.value = '';
  handleImageSrcChange(); // TODO refactor
  emit('setMode', newMode);
};
const printLabel = () => window.print();
</script>

<style scoped>
.controls {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.tabs {
  display: flex;
  flex-direction: row;
  width: 100%;
  justify-content: space-between;
}

.tabs__item {
  border-bottom: 1px dashed gray;
}

.tabs__item--active {
  border-bottom: none;
  font-weight: bold;
}
</style>
