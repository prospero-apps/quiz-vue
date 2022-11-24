<script setup>
  import q from '../data/quizzes.json'
  import { ref, watch } from 'vue'
  import Category from '../components/Category.vue'

  const quizzes = ref(q)
  const search = ref('')

  watch(search, () => {
    quizzes.value = q.filter(quiz => quiz.category.toLowerCase().includes(search.value.toLowerCase()))
  })
</script>

<template>
  <div>
    <header>
      <h1>Quizzes</h1>
      <input v-model.trim="search" type="text" placeholder="Search...">
    </header>
    <div class="categories-container">
      <Category v-for="quiz in quizzes" :key="quiz.id" :quiz="quiz" />
    </div>
  </div>
</template>

<style scoped>
.body {
  margin: auto;
}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px;
  gap: 40px;
  margin-bottom: 10px;
  background-color: silver;
}

header h1 {
  font-size: 50px;
  font-weight: bold;
}

input[type=text] {
  font-size: 30px;
  padding: 10px;
  border: none;
  border-radius: 5px;
}

.categories-container {
  padding: 20px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  gap: 40px;
}

@media screen and (max-width: 700px) {
  header {
    flex-direction: column;
    gap: 0;
  }
}
</style>
