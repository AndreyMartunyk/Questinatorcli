<template>
  <div>
    <h1>questionList</h1>
    <ul>
        <QuestionItem
        v-for="item in questions"
        :key="item.QuestionId"
        v-bind:question="item"
        />
        
    </ul>
  </div>
</template>

<script>
import QuestionItem from "@/components/QuestionItem.vue"
export default {
  props:[
    'questions'
  ],
    components: {
        QuestionItem,
    }

};
</script>

<style>
</style>