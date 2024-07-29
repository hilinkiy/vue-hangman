<script setup>
import "./assets/style.css"
import onKeydown from './assets/onKeydown.js'
import {computed, ref} from "vue";
import Header from "./components/Header.vue";
import Figure from "./components/Figure.vue";
import WrongLetters from "./components/WrongLetters.vue";
import Word from "./components/Word.vue";
import Popup from "./components/Popup.vue";
import Notification from "./components/Notification.vue";

let words = ['programming', 'vue', 'react', 'games', 'pie', 'code', 'football', 'basketball', 'computer', 'note']
const randomWord = () => words[Math.floor(Math.random() * words.length)]

const letters = computed(() => word.value.split(''))
const guessedLetters = ref([])
const word = ref(randomWord())
const wrongLetters = computed(() => guessedLetters.value.filter(l => !letters.value.includes(l)))
const correctLetters = computed(() => guessedLetters.value.filter(l => letters.value.includes(l)))

const status = computed(() => {
  if (wrongLetters.value.length === 6) return 'lose'
  if (letters.value.every(l => correctLetters.value.includes(l))) return 'win'
})

const reset = () => {
  guessedLetters.value = []
  words = randomWord()
}

const notification = ref(false)
const showNotification = () => {
  notification.value = true
  setTimeout(() => (notification.value = false), 2000)
}

onKeydown(event => {
  const letter = event.key.toLowerCase()
  if (event.keyCode < 65 && event.keyCode > 90) return
  if (status.value) return
  if (guessedLetters.value.includes(letter)) {
    showNotification()
    return
  }
  guessedLetters.value.push(letter)
})
</script>

<template>
  <div class="wrapper">
    <Header/>
    <Figure :wrongCount="wrongLetters.length"/>
    <WrongLetters :wrong-letters="wrongLetters"/>
    <Word :letters="letters" :correct-letters="correctLetters"/>
    <Popup :status="status" :word="word" @reset="reset"/>
    <Notification :show="notification"/>
  </div>
</template>

<style scoped>

</style>