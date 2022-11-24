<script setup>
  import { defineProps } from 'vue'

  const { question } = defineProps(['question'])
</script>

<template>
  <div class="question">
    <h2 class="question-text">
      {{ question.questionText }}
    </h2>
    <div class="options">
      <div 
        v-for="option in question.options" 
        :key="option.id"
        class="option"
      >
        <p class="option-label">{{ option.label }}</p>
        <p class="option-text">{{ option.optionText }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .option-label {
    border: 4px solid #2c3e50;
    border-radius: 50%;
    font-weight: bold;
    width: 2em;
    height: 2em;
    display: grid;
    justify-content: center;
    align-content: center;
  }
  
  .question-text {
    font-size: 40px;
    margin-top: 40px;
    margin-bottom: 50px;
  }

  .options {
    display: flex;
    flex-direction: column;
    font-size: 30px;
    gap: 1em;
  }

  .option {
    display: flex;
    align-items: center;
    background-color: rgb(243, 236, 236);
    gap: 1em;
    padding: 5px;
  }

  .option:hover {
    background-color: rgb(247, 243, 243);
  }

  .option-label {
    border: 2px solid #2c3e50;
    border-radius: 50%;
    width: 2em;
    height: 2em;
  }
</style>