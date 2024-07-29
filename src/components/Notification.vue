<script setup>
const props = defineProps({
  show: {
    type: Boolean,
    default: false
  }
})
</script>

<template>
<div class="notification-container" :class="show ? 'show' : ''">
  <p>You already entered this letter</p>
</div>
</template>

<style scoped>

</style>