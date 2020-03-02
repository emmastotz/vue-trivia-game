<template>
  <div>
    <button class="bg-gray-600 text-white rounded m-4 py-1 px-2 shadow" @click= "next" > Submit Answer </button>
    <form id="q-form">
    <section class="text-white m-8">
      <div v-if="questions[index] != undefined">
        <p> {{ questions[index].id }}.{{ questions[index].questionValue }}</p>
        <div v-for="option in questions[index].options" :key="option.key" class="custom-control custom-radio custom-control-inline">
          <input type="radio" :id= "option.key" :value= "option.truthValue" class="custom-control-input" :for="questions[index].id" :name="questions[index].id">
          <label :for= "option.key" class="custom-control-label"> {{option.optionValue}}  </label>
        </div>
      </div>
    </section>
    </form>
  </div>
</template>

<script>
import questions from "@/util/questions.js";

export default {
  data() {
    return {
      index: 0
    };
  },
  mounted() {
    this.index = 0
  },
  props: {
    questions: {
      type: Array,
      required: true
    }
  },
  methods: {
    next(){
      this.index++;
    }
  }
};
</script>