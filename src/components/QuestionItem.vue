<template>
  <div class="card">
    <div class="user">
      <img :src="user.photo" class="userIcon" alt="Photo" />
      <div class="userName">{{user.nickName}}</div>
    </div>
    <div class="content">
      <div class="question">
        <p>{{ question.questionMessage }}</p>
      </div>
      <div class="answers">
        <AnswerLine v-for="answer in question.answers" :key="answer.answerId">{{ answer.answerMsg }}</AnswerLine>
      </div>
      <button disabled>Добавить свой вопрос</button>
      <button>Confirm</button>
    </div>
  </div>
</template>


<script>
import AnswerLine from "@/components/AnswerLine.vue";
export default {
  components: {
    AnswerLine
  },
  props: {
    question: {
      type: Object,
      required: true
    },
    user: {
      type: Object,
      required: true
    }
  },
  data() {
    return {};
  }
};
</script>


<style scoped>
button{
  padding: 8px 15px 8px 15px;
  margin-left: 10px;
  margin-right: 10px;
  border-radius: 5px;
  margin-bottom: 15px;
}

.content{
  width: 580px;
  margin-right: 10px;
}
.answers {
  padding: 10px;
}
.question {
  padding: 20px 20px 20px 20px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  margin-top: 10px;
  margin-bottom: 20px;
  background-color:#1abc9cb4;
  color: white;
  font-size: 1.3rem;
}
.card {
  display: flex;
  justify-content: space-between;;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  max-width: 700px;
  margin: auto;
  text-align: center;
  padding: 5px;
  margin-bottom: 15px;
  margin-top: 15px;
}
.user {
  margin: 10px;
}
.userIcon {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  border-radius: 50%;
  margin-bottom: 10px;
  width: 70px;
  height: 70px;
}

</style>