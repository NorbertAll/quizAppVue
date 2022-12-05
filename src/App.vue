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
    if(q.selected!=null && q.answer == q.selected){
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
  questions.value[currentQuestion.value].selected=e.target.value
  e.target.value=null
}
const NextQuestion=()=>{
  if(currentQuestion.value<questions.value.length - 1){
    currentQuestion.value++
    return
  }
    quizCompleted.value=true
  
}
</script>

<template>
  <main class="app">
    <h1>QUIZ</h1>
    <section class="quiz" v-if="!quizCompleted">
      <div class="quiz-info">
        <span class="question"> {{ getCurrentQuestion.question }}                </span>
        <span class="score">     Score {{score}}/{{questions.length}}            </span>
      </div>
      <div class="options">
        <label v-for="(option, index) in getCurrentQuestion.options" :for="'option'+index" :class="`option ${
          getCurrentQuestion.selected==index
            ?index==getCurrentQuestion.answer 
              ? 'correct' :'wrong'
            :''
        }${
          getCurrentQuestion.selected !=null &&
          index != getCurrentQuestion.selected
            ?'disable'
            :''
        }`">
          <input type="radio" 
          :id="'option'+index"
          :name="getCurrentQuestion.index" 
          :value="index" 
          v-model="getCurrentQuestion.selected"
          :disabled="getCurrentQuestion.selected"
          @change="SetAnswer">
          <span>{{option}}</span>
        </label>
      </div>
      <button
        @click="NextQuestion"
        :disable="!getCurrentQuestion.selected">
        {{
          getCurrentQuestion.index == questions.length - 1
            ?'Finish'
            :getCurrentQuestion.selected ==null
              ?'Wybierz odpowiedź'
              :'Następne pytanie'
        }}
        
       
      </button>
    </section>
    <section v-else>
      <h2>Skończyłeś test</h2>
      <p>Twój wynik to: {{score}}/{{questions.length}}</p>

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
  background-color: #e4f1fe;
  color: black;
}
.app{
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
  min-height: 100vh;
}
h1{
  font-size: 2rem;
  margin-bottom: 2rem;
}
.quiz{
  background-color: #8dc6ff;
  padding: 1rem;
  width: 100%;
  max-width: 640px;
  border-radius: 0.5rem;
}
.quiz-info{
  display: flex;
  justify-content: space-between;
  gap: 2rem;
  margin-bottom: 1rem;
}
.quiz-info .question{
  color: #22313f;
  font-size: 1.25rem;
}
.quiz-info .score{
  color: #34495e;
}
.options{
  margin-bottom: 1rem;
}
.option{
  display: block;
  color: white;
  padding: 1rem;
  background-color: #34495e;
  margin-bottom: 0.5rem;
  border-radius: 0.5rem;
  cursor: pointer;
}
.option:hover{
  color: black;
  background-color: #e4f1fe;
}
.option.correct{
  background-color: #2cce7d;
}
.option.wrong{
  background-color: red;
}
.option:last-of-type{
  margin-bottom: 0;
}
.option.disable{
  opacity: 0.5;
}
.option input{
  display: none;
}
button{
  appearance: none;
  outline: none;
  border:none;
  cursor: pointer;
  padding: 0.5rem 1rem;
  background-color: #2cce7d;
  color: #2d213f;
  font-weight: 700;
  text-transform: uppercase;
  font-size: 1.25rem;
  border-radius: 0.5rem;
}
button:disabled {
  opacity: 0.5;
}
h2{
  font-size: 2rem;
  margin-bottom: 2rem;
  text-align: center;
}
p{
  font-size: 1.25rem;
  text-align: center;
}
</style>
