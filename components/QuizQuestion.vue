<template>
  <section>
    <form id="q-form">
      <div class="text-white m-8 blue rounded-lg shadow px-6 pt-4">
        <div v-if="questions[index] != undefined">
          <p>{{ questions[index].id }}. {{ questions[index].questionValue }}</p>
          <div v-for="option in questions[index].options" :key="option.key" class>
            <label :for="option.key">
              <input
                type="radio"
                :id="option.key"
                :value="option.optionValue"
                :name="questions[index].id"
                v-model="userCurrentResponse"
                >
                  {{option.optionValue}}
            </label>
          </div>
        </div>
        <button
          class="bg-gray-600 text-white rounded m-4 py-1 px-2 shadow focus:outline-none hover:bg-gray-700"
          @click.prevent="next"
        >Submit </button>
      </div>
    </form>
  </section>
</template>
<script>
import questions from "@/util/questions.js";

export default {
  data() {
    return {
      index: 0,
      userCurrentResponse: "a",
      userResponses: []
      };
  },
  mounted() {
    this.index = 0,
    this.choice = "a"
  },
  props: {
    questions: {
      type: Array,
      required: true
    }
  },
  methods: {
    next() {
      this.index++;
      this.userResponses.push(this.userCurrentResponse)
    }
  }
};
</script>