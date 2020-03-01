<template>
  <div
    class="p-8 flex flex-col w-full antialiased text-center items-center justify-center"
  >
  <div> 
    <QuestionTimer :time-left="timeLeft" :time-limit="timeLimit" />
  </div>
    <QuizQuestion :questions="questions"/>
  </div>
</template>

<script>
import QuestionTimer from "@/components/QuestionTimer";
import QuizQuestion from "@/components/QuizQuestion";
import questions from "@/util/questions.js";

const TIME_LIMIT = 20;

export default {
  components: {
    QuestionTimer,
    QuizQuestion
  },

  data() {
    return {
      timePassed: 0,
      timerInterval: null,
      questions: []
    };
  },

  computed: {
    timeLimit() {
      return TIME_LIMIT;
    },

    timeLeft() {
      return this.timeLimit - this.timePassed;
    }
  },

  watch: {
    timeLeft(newValue) {
      if (newValue === 0) {
        this.onTimesUp();
      }
    }
  },

  mounted() {
    this.startTimer();
    this.questions = questions.questions;
  },

  methods: {
    onTimesUp() {
      clearInterval(this.timerInterval);
    },

    startTimer() {
      this.timerInterval = setInterval(() => (this.timePassed += 1), 1000);
    }
  }
};
</script>
