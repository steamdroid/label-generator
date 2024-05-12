<template>
  <main class="container">
    <PosLabel :mode="mode" :title="title" :description="description" :icon="icon" />
    <LabelControls
      :mode="mode"
      @setTitle="(input) => (title = input)"
      @setDescription="(input) => (description = input)"
      @setImageSrcString="(input) => (imageSrcString = input)"
      @setMode="(val) => (mode = val)"
    />
  </main>
</template>
<script setup>
import { ref, watch } from 'vue';
import PosLabel from '@/components/PosLabel.vue';
import LabelControls from '@/components/LabelControls.vue';

import QRCode from 'qrcode';

const mode = ref('pic');
const title = ref('');
const description = ref('');
const imageSrcString = ref('');
const icon = ref('');

watch([mode, imageSrcString], async () => {
  switch (mode.value) {
    case 'pic':
      icon.value = imageSrcString.value;
      break;
    case 'qr':
      if (imageSrcString.value === '') {
        icon.value = '';
      } else {
        icon.value = await QRCode.toDataURL(imageSrcString.value);
      }
      break;
  }
});
</script>
