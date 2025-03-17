<template>
  <div class="flex flex-col items-center justify-center mt-4 gap-4">
    <SpeechBubble position="b" color='yellow' shape="round" maxWidth="160px" textAlign="center">
      <p class="text-xs">{{ props.text }}</p>
    </SpeechBubble>
    <img src="/images/UsagiItem2e.png" width="120px"/>
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  text: '',
})
</script>