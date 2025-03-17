<template>
  <div class="flex flex-col items-center justify-center mt-4 gap-6">
    <SpeechBubble position="b" color='pink' shape="round" maxWidth="160px" textAlign="center">
      <p class="text-xs">{{ props.text }}</p>
    </SpeechBubble>
    <img src="/images/ChiikawaItem2e.webp" width="80px"/>
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  text: '',
})
</script>