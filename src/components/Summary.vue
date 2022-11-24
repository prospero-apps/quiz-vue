<script setup>
  import { defineProps } from 'vue'
  import { computed } from 'vue';
  import { RouterLink } from 'vue-router'

  const { numberOfQuestions, numberOfCorrectAnswers } = defineProps(["numberOfQuestions", "numberOfCorrectAnswers"])
  const result = computed(() => numberOfCorrectAnswers / numberOfQuestions)
  const resultText = computed(() => {
    if (result.value > 0.9) return 'Excellent!'
    else if (result.value > 0.75) return 'Good job!'
    else if (result.value > 0.5) return 'You could have done better.'
    else if (result.value > 0.25) return 'You did rather poorly.'
    return 'Seriously? Are you that bad?'
  })
</script>

<template>
  <div class="summary">
    <h1>Summary</h1>
    <div class=result>
      Your score is {{ numberOfCorrectAnswers }} / {{ numberOfQuestions }}.
    </div>
    <div class="result-text">
      {{ resultText }}
    </div>
    <RouterLink class="back" to="/">Go back to the quizzes</RouterLink>
  </div>
</template>

<style scoped>
.summary {
    text-align: center;    
  }

  h1 {
    font-size: 100px;
    font-weight: bold;
  }

  .result {
    font-size: 40px;
  }

  .result-text {
    font-size: 30px;
    margin-bottom: 50px;
  }

  .back {
    margin: 10px 10px;
    background-color: #2c3e50;
    padding: 10px;
    border: none;
    color: white;
    font-size: 20px;
    text-decoration: none;
  }

  .back:hover {
    background-color: #485868;
  }
</style>