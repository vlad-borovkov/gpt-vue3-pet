<script setup>
import {ref} from "vue";
const _inputPrompt = ref('');
import OpenAI from "openai";

defineProps({
  msg: {
    type: String,
    required: true
  }
})
const emit = defineEmits(['renderAnswer'])

const openai = new OpenAI({
  apiKey: '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',
  dangerouslyAllowBrowser: true,
});

const sendPrompt = async () => {
  const completion = await openai.chat.completions.create({
    messages: [
      { role: "system", content: "You are a helpful assistant. Get Answer on Russian" },
      { role: 'user', content: _inputPrompt.value},
    ],
    model: "gpt-3.5-turbo",
  });
  emit('renderAnswer', completion.choices[0].message.content);

}
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <div class="prompt__form"
    >
      <label for="enterPrompt"></label>
      <form
          class="prompt__input-wrp"
          @submit.prevent>
        <textarea
            class="prompt__input"
            v-model="_inputPrompt"
            @keydown.enter="sendPrompt"
        />
        <button
            :disabled="_inputPrompt === ''"
            @click="sendPrompt"
            class="prompt__button"
        >Get result</button>
      </form>
    </div>


  </div>
</template>

<style scoped lang="scss">
.prompt {
  &__form {
    display: flex;
    flex-direction: column;
  }
  &__input-wrp {
    position: relative;
    display: flex;
  }
  &__input {
    background-color: rgba(255, 255, 255, 0.9);
    border-color: #75ac9d;
    border-radius: 10px;
    height: 100px;
    width: 100%;
    resize: none;
    font-size: 16px;
  }
  &__button {
    position: absolute;
    right: 2%;
    bottom: 5%;
    background-color: #75ac9d;
    border-radius: 10px;
  }
}
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
