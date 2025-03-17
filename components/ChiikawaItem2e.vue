<template>
  <div class="flex flex-col items-center justify-center mt-4 gap-6">
    <SpeechBubble position="b" color='pink' shape="round" maxWidth="200px" textAlign="center">
      {{props.text}}
    </SpeechBubble>
    <img src="/images/ChiikawaItem2e.webp" width="100px"/>
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  text: '',
})
</script>