<template>
<div  v-if="!quizStarted" >
  <h1 class="text-center">日向坂46に関するクイズです</h1>
  <h2 class="text-center">ぜひ挑戦してみてください。</h2>
  <div class="d-grid gap-2 col-6 mx-auto">
    <button class="btn btn-primary" @click="startQuiz">スタート！</button>
  </div>
</div>
<div v-else-if="!quizFinished">
  <h2 class="mb-4">{{ currentQuestion.id }}.{{ currentQuestion.question }}</h2>
  <div class="btn-group d-grid gap-3">
    <button v-for="(option, index) in currentQuestion.options" :key="index" class="btn btn-outline-primary" @click="answerQuestion(option)">
      {{ option }}
    </button>
  </div>
</div>
</template>

<script>
export default {
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
