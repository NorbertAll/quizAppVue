<script setup>
import {ref, computed} from 'vue'

const questions=ref([
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
  let value=0
  questions.value.map(q=>{
    if(q.selected==q.answer){
      value++
    }
  })
  return value
})

const getCurrentQuestion=computed(()=>{
  let question = questions.value[currentQuestion.value]
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
  <main class="app">
    <h1>QUIZ</h1>
    <section class="quiz">
      <div class="quiz-info">
        <span class="question"> {{ getCurrentQuestion.question }} </span>
        <span class="score">Score {{score}}/{{questions.length}}</span>
      </div>
      <div class="options">
        <label v-for="(option, index) in getCurrentQuestion.options" :key="index" :class="`option ${
          getCurrentQuestion.selected==index
            ?index=getCurrentQuestion.answer 
              ? 'correct' :'wrong'
            :''
        }${
          getCurrentQuestion.selected !=null &&
          index != getCurrentQuestion.selected
            ?'disable'
            :''
        }`">
          <input type="radio" 
          :name="getCurrentQuestion.index" 
          :value="index" 
          v-model="getCurrentQuestion.selected"
          :disabled="getCurrentQuestion.selected"
          @change="SetAnswer">
          <span>{{option}}</span>
        </label>
      </div>
      
    </section>
   
  </main>
</template>

<style>
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
