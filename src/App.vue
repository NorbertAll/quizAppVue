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
const quizCompleted=ref(false)
const currentQuestion=ref(0)
const score =computed(()=>{
  let value=0;
  question.value.map(q=>{
    if(q.selected==q.answer){
      value++
    }
  })
  return value;
})

const getCurrentQuestion=computed(()=>{
  let question = question.value[currentQuestion.value]
  question.index=currentQuestion.value
  return question
})
const SetAnswer=e=>{
  question.value[currentQuestion.value].selected=e.target.value
  e.target.value=null
}
const NextQuestion=()=>{
  if(currentQuestion.value<question.value.length - 1){
    currentQuestion.value++
  }else{
    quizCompleted.value=true
  }
}
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
