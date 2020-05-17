<template>
  <div>
    <input v-model="answer" @input="$emit('input', answer, index)" />
    <button @click="answer = ''">Clear</button>
  </div>
</template>

<script>
export default {
  props: {
    index: {
      type: Number,
      required: false
    }
  },
  data() {
    return {
      answer: ""
    };
  }
};
</script>

<style scoped>
button {
  width: 200px;
}
</style>