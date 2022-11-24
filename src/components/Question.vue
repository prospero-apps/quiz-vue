<script setup>
  import { defineProps, defineEmits } from 'vue'

  const { question } = defineProps(['question'])
  const emit = defineEmits(['selectOption'])

  const emitSelectedOption = (option) => {
    const yourOptionLabel = option.label
    emit('selectOption', option.correct, yourOptionLabel)
  }
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
        @click="emitSelectedOption(option)"
      >
        <p class="option-label">{{ option.label }}</p>
        <p class="option-text">{{ option.optionText }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
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
    cursor: pointer;
  } 

  .option-label {
    border: 2px solid #2c3e50;
    border-radius: 10%;
    font-weight: bold;
    width: 2em;
    height: 2em;
    min-width: 2em;
    min-height: 2em;
    display: grid;
    justify-content: center;
    align-content: center;
  }

  .correct,
  .correct:hover {
    border: 2px solid green;
    border-radius: 5px;
    background-color: rgb(215, 240, 215);
  }

  .incorrect,
  .incorrect:hover {
    border: 2px solid red;
    border-radius: 5px;
    background-color: rgb(243, 212, 212);
  }
  
</style>