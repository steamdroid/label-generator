<template>
  <section class="pos-label">
    <div class="pos-label__pic">
      <i v-if="mode === 'pic'" :class="'las la-' + icon"></i>
      <img v-else-if="mode === 'qr'" :src="icon" />
    </div>
    <div class="pos-label__text">
      <h1 class="pos-label__title">{{ title }}</h1>
      <p class="pos-label__desc">{{ description }}</p>
    </div>
  </section>
</template>
<script setup>
defineProps({
  mode: String,
  title: String,
  description: String,
  icon: String
});
</script>
<style scoped>
.pos-label {
  display: flex;
  flex-direction: row;
  width: 240px;
  font-size: 12px;
  font-family: 'Times New Roman';
  padding: 12px 5px;
  word-break: break-all;
  line-height: 1.1em;
  border: 1px dashed gray;
}

.pos-label__title {
  font-weight: bold;
  font-size: 1.4em;
  line-height: 1em;
  margin: 0;
  margin-bottom: 10px;
  max-width: 142px;
}

.pos-label__desc {
  font-size: 1em;
  line-height: 1em;
  margin: 0;
  max-width: 140px;
}

.pos-label__pic {
  width: 64px;
  height: 64px;
  font-size: 64px;
  margin-right: 15px;
}

.pos-label__pic i {
  color: black;
}
</style>
