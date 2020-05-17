<template>
  <div class="createF">
    <textarea placeholder="enter the question" v-model="questionMessage"></textarea>
    <div class="create-form-options">
      <div class="quest">
        <label for="is-self-answer">Возможность оставлять свои варианты ответов</label>
        <input class="checkB" type="checkbox" id="is-self-answer" v-model="isSelfAnswer" />
      </div>
      <template v-if="isSelfAnswer">
        <div class="quest">
          <span>Выберите максимальное колличество кастомных вопросов:</span>
          <select v-model.number="countOfCustomAnswers">
            <option value="0">Выберите число</option>
            <option>1</option>
            <option>2</option>
            <option>3</option>
            <option>4</option>
          </select>
        </div>
      </template>

      <div class="quest">
        <span>За сколько вариантов можно проголосовать</span>
        <select v-model.number="maxAnswers">
          <option value="1">1</option>
          <option>2</option>
          <option>3</option>
          <option>4</option>
        </select>
      </div>
      <div class="quest">
        <span>Дедлайн для ответов</span>
        <input type="datetime-local" v-model="answerDeadline" />
      </div>
      <h3>Answers:</h3>

      <AnswersInputList :countOfAnswers="5" @input="getAnswers" />
    </div>
    <div>
      <button @click="createQuestion(false)">Send</button>
      <button @click="createQuestion(true)">Save</button>
    </div>
  </div>
</template>



<script>
import AnswersInputList from "@/components/AnswersInputList.vue";

export default {
  data() {
    return {
      isSelfAnswer: false,
      countOfCustomAnswers: 0,
      maxAnswers: 1,
      answers: [],
      // countOfAswers: 1,
      answerDeadline: "",
      questionMessage: ""
    };
  },
  computed: {
    getCountOfCustomAnswers() {
      if (!this.isSelfAnswer) {
        return 0;
      } else {
        return this.countOfCustomAnswers;
      }
    }
  },
  methods: {
    getAnswers(data) {
      // console.log(data);

      this.answers = data;
    },
    createQuestion(isSaved) {
      let question = {
        UserOwnerId: 1,
        QuestionMessage: this.questionMessage,
        CreateDate: "",
        AnswerDeadline: this.answerDeadline,
        MaxCustomQuestions: this.getCountOfCustomAnswers,
        MaxAnswers: this.maxAnswers,
        IsSaved: isSaved,
        IsActive: true,
        Answers: this.answers
      };

      console.log("emit -", question);
      this.$emit("addQuestion", question);
    }
  },
  components: {
    AnswersInputList
  }
};
</script>

<style>
.createF {
  background-color: rgb(132, 182, 131);
}
.createF textarea {
  width: 400px;
  margin-top: 15px;
  padding: 7px;
  border-radius: 5px;
}
.createF button {
  margin: 10px;
  width: 100px;
  height: 30px;
  border-radius: 5px;
}
.createF select {
  padding-left: 10px;
}
.createF input {
  margin: 5px;
  padding: 5px;
}
.quest {
  margin: 5px;
  padding: 5px;
}
.createF .checkB {
  transform: scale(1.3);
}
</style>