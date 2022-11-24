<script setup>
  import { defineProps } from 'vue'
  import { useRouter } from 'vue-router'

  const { quiz } = defineProps(['quiz'])
  const router = useRouter()

  const goto = () => {
    router.push(`/quiz/${quiz.id}`)
  }
</script>

<template>
  <div class="category" @click="goto">
    <img 
      :src="quiz.img" 
      :alt="quiz.category">
    <div class="category-name">
      <h2>{{ quiz.category }}</h2>
      <p>{{ quiz.questions.length }} questions</p>
    </div>
  </div>
</template>

<style scoped>
  .category {
    width: 300px;
    overflow: hidden;
    box-shadow: 2px 2px 10px silver;
    cursor: pointer;
  }

  .category img {
    width: 100%;
    height: 160px;
  }

  .category-name {
    padding: 0 5px;
  }

  .category-name h2 {
    font-weight: bold;
  }
</style>