<template>
  <div>
    <h1>questionList</h1>
    <ul>
      <QuestionItem
        v-for="item in questions"
        :key="item.QuestionId"
        v-bind:question="item"
        v-bind:user="getUser(item.UserOwnerId)"
      />
    </ul>
  </div>
</template>

<script>
import QuestionItem from "@/components/QuestionItem.vue";
export default {
  props: {
    questions: {
      type: Array,
      required: true
    },
    users: {
      type: Array,
      required: true
    }
  },
  methods: {
    getUser(userId) {
      return this.users.find(user => user.UserOwnerId == userId);
    }
  },
  computed: {},
  components: {
    QuestionItem
  }
};
</script>

<style>
</style>