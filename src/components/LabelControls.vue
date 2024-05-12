<template>
  <section class="controls no-print">
    <div class="controls__tabs tabs">
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
    <input @input="handleTitleChange" type="text" name="title" placeholder="Название" />
    <input @input="handleDescriptionChange" type="text" name="desc" placeholder="Описание" />
    <input
      @input="handlePicChange"
      type="text"
      name="pic"
      :placeholder="mode === 'pic' ? 'Иконка' : 'Ссылка'"
    />
    <button type="button" @click="printLabel">Напечатать</button>
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

const emit = defineEmits(['setTitle', 'setDescription', 'setPic', 'setMode']);
const handleTitleChange = (e) => {
  emit('setTitle', e.target.value);
};
const handleDescriptionChange = (e) => {
  emit('setDescription', e.target.value);
};
const handlePicChange = (e) => {
  emit('setPic', e.target.value);
};
const handleModeChange = (newMode) => {
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
