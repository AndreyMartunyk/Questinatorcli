<template>
  <div>
    <AnswerInput v-for="index in countOfAnswers" :key="index" :index="index" @input="getInput" />
  </div>
</template>

<script>
import AnswerInput from "@/components/AnswerInput.vue";
export default {
  components: {
    AnswerInput
  },
  data() {
    return {
      answers: []
    };
  },
  props: {
    countOfAnswers: {
      type: Number,
      required: true
    }
  },
  methods: {
    getInput(value, index) {
      this.answers[index - 1] = { AnswerMsg: value };
      this.$emit("input", this.answers);
    }
  }
};
</script>

<style>
</style>