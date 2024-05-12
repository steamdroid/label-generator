<template>
  <main class="container">
    <PosLabel :mode="mode" :title="title" :description="description" :icon="icon" />
    <LabelControls
      :mode="mode"
      @setTitle="(input) => (title = input)"
      @setDescription="(input) => (description = input)"
      @setPic="(input) => (pic = input)"
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
const pic = ref('');
const icon = ref('');

watch([mode, pic], async () => {
  switch (mode.value) {
    case 'pic':
      icon.value = pic.value;
      break;
    case 'qr':
      if (pic.value) {
        icon.value = await QRCode.toDataURL(pic.value);
      }
      break;
  }
});
</script>
