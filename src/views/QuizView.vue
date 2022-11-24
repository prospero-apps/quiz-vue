<script setup>
  import Question from '../components/Question.vue'  
  import { useRoute } from 'vue-router'
  import { ref, computed } from 'vue'
  import quizzes from '../data/quizzes.json'
  import Summary from '../components/Summary.vue'

  const route = useRoute()
  const quizId = parseInt(route.params.id)
  const currentQuiz = quizzes.find(quiz => quiz.id === quizId)
  const currentQuestionIndex = ref(0)
  const numberOfCorrectAnswers = ref(0)
  const buttonDisabled = ref(true)
  const yourAnswerText = ref('')
  const correctAnswerText = ref('')
  const quizFinished = ref(false)

const buttonText = computed(() => currentQuestionIndex.value + 1 < currentQuiz.questions.length ? 'Next Question' : 'See Summary')
  
  const onOptionSelected = (correct, yourAnswer) => {
    if (yourAnswerText.value === '') {
      yourAnswerText.value = `Your answer: ${yourAnswer}`
      const correctAnswer = currentQuiz.questions[currentQuestionIndex.value].options.find(o => o.correct).label
      correctAnswerText.value = `Correct answer: ${correctAnswer}`

      if (correct) {
        numberOfCorrectAnswers.value++
      }

      buttonDisabled.value = false      
    }  
  }

  const moveOn = () => {  
    currentQuestionIndex.value++
    buttonDisabled.value = true
    yourAnswerText.value = ''
    correctAnswerText.value = ''   
    
    if (currentQuestionIndex.value === currentQuiz.questions.length) {
      quizFinished.value = true
    }
  }
  
</script>

<template>  
  <div class="question-container"> 
    <div class="content-container" v-if="!quizFinished">
      <div>
        <header>
          <h1>{{ currentQuiz.category }}</h1>
          <div class="progress">
            <div v-for="question in currentQuiz.questions">
              <div v-if="question.id < currentQuestionIndex + 1" class="question-number answered">{{ question.id }}</div>
              <div v-else class="question-number">{{ question.id }}</div>
            </div>
          </div>
        </header>
        <div>
          <Question      
            :question="currentQuiz.questions[currentQuestionIndex]"            
            @selectOption="onOptionSelected"
          />      
        </div>
      </div>
      <div class="footer">
        <div class="info">
          <p>{{ yourAnswerText }}</p>
          <p>{{ correctAnswerText }}</p>
        </div>
        <p>Number of correct answers so far: {{ numberOfCorrectAnswers }}</p>
        <button
          :disabled="buttonDisabled"
          @click="moveOn"
        >
          {{ buttonText }}
        </button>        
      </div>
    </div>
    <Summary 
      v-else 
      :numberOfQuestions="currentQuiz.questions.length"
      :numberOfCorrectAnswers="numberOfCorrectAnswers"
    />
  </div>
</template>

<style scoped>
.question-container {
    padding: 0 20px;
    height: 100vh;
  }

  .content-container {
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  
  header h1 {
    font-size: 60px;
    font-weight: bold;
  }

  .progress {
    display: flex;
    flex-wrap: wrap;
    font-size: 2em;
    gap: 10px;
    padding: 20px 0;
  }

  .question-number {
    border: 4px solid #2c3e50;
    border-radius: 50%;
    font-weight: bold;
    width: 2em;
    height: 2em;
    display: grid;
    justify-content: center;
    align-content: center;
  }

  .answered {
    background-color: #2c3e50;
    color: white;
  }

  .footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 10px;
  }

  button {
    margin: 10px 10px;
    background-color: #2c3e50;
    padding: 10px;
    border: none;
    color: white;
    font-size: 20px;
  }

  button:hover {
    background-color: #485868;
  }

  button:disabled {
    background-color: #d0d1d3;
  }
</style>