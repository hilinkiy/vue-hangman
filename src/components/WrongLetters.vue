<script setup>
  const props = defineProps({
    wrongLetters: {
      type: Array,
      default: () => []
    }
  })
</script>

<template>
  <div class="wrong-letters-container">
    <div class="wrong-letters">
      <p v-show="wrongLetters.length > 0">
        Wrong
        <span v-for="(letter, i) in wrongLetters" :key="letter">
          {{letter}}
          {{i === wrongLetters.length - 1 ? '' : ', '}}
        </span>
      </p>
    </div>
  </div>
</template>

<style scoped>

</style>