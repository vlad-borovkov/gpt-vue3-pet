<script setup>
import PromptArea from './components/PromptArea.vue'
import {reactive} from "vue";

const gptAnswers = reactive([])
const renderAnswer = (answer) => {
  gptAnswers.push({
    id: Math.random(),
    answer
  })

}

</script>

<template>
  <header>
<!--    Добавить лого GPT-->
    <img alt="GPT logo" class="logo" src="./assets/ChatGPT_logo.png" width="125" height="125" />

    <div class="wrapper">
      <PromptArea
          msg="Enter a prompt for GPT!"
          @renderAnswer="renderAnswer"
      />
    </div>
  </header>
<main>
<!--  //Здесьс список ответов от чата-->

  <ul class="answer__list">
    <li
        v-for="answer in gptAnswers"
        :key="answer?.id"
    >
      <details>
        <summary>Ответ № {{answer?.id}}</summary>
        <p>{{answer?.answer}}</p>
      </details>
    </li>
  </ul>
</main>
</template>

<style scoped lang="scss">
.answer {
  &__list {
    max-height: 70vh;
    overflow-y: scroll;
    list-style-type: none;
  }
}
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
