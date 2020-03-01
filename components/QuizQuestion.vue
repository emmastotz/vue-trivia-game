<template>
  <section class="text-white m-8">
    <div v-for="question in questions" :key="question.id">
      {{ question.id }}.
      {{ question.questionValue }}
      <div v-for="option in question.options" :key="option.key">
        {{ option.optionValue }}
      </div>
    </div>
  </section>
</template>

<script>
import questions from "@/util/questions.js";

export default {
  props: {
    questions: {
      type: Array,
      required: true
    }
  }
};
</script>
