<script setup>
  import Question from '../components/Question.vue'  
  import { useRoute } from 'vue-router'
  // import { ref, computed } from 'vue'
import { ref } from 'vue'
  import quizzes from '../data/quizzes.json'

  const route = useRoute()
  const quizId = parseInt(route.params.id)
  const currentQuiz = quizzes.find(quiz => quiz.id === quizId)
  const currentQuestionIndex = ref(0)
  // const questionAnswered = computed(() => {
  //   return currentQuestionIndex.value
  // })
</script>

<template>  
  <div class="question-container">
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
      />
    </div>
    <button @click="currentQuestionIndex++">Next</button>
  </div>
</template>

<style scoped>
  .question-container {
    padding: 0 20px;
    max-height: 90vh;
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
</style>