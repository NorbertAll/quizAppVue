<script setup>
import {ref, computed} from 'vue'

const question=ref([
  {
    question: 'Framework backendowy w którym piszemy w Pythonie?',
    answer: 0,
    options:['Django', 'Laravel', 'Symfony'],
    selected: null
  },
  {
    question: 'Bibliotego frontendowa w której piszem w TS lub JS?',
    answer: 2,
    options:['Django', 'Laravel', 'React'],
    selected: null
  },
  {
    question: 'Framework backendowy w którym piszemy w PHP?',
    answer: 1,
    options:['Django', 'Laravel', 'React'],
    selected: null
  }
])
</script>

<template>
  <h1>Hel</h1>
</template>

<style scoped>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Montserrat', sans-serif;
}
body{
  background-color: rgba(240, 248, 255, 0.163);
  color: black;
}
</style>
