<template>
  <div class="home">
    <Header></Header>

    <div class="content">
      <CreateForm
      @addQuestion="addQuestion"
      />
      <QuestionList 
      v-bind:questions="questions" 
       />
    </div>

    <Footer></Footer>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import Footer from "@/components/Footer.vue";
import Header from "@/components/Header.vue";
import CreateForm from "@/components/CreateForm.vue";
import QuestionList from "@/components/QuestionList.vue";

export default {
  name: "Home",
  components: {
    //HelloWorld
    Footer,
    Header,
    CreateForm,
    QuestionList
  },
  mounted: function() {
    this.getQuestions();
    this.getUsers();
  },
  data() {
    return {
      questions: [],
      users: [],
      currentUser: {
        userOwnerId: 1 //hardcode - потом должно зависеть от пользователя
      }
    };
  },
  methods: {
    getUsers() {
      //need chek
      console.log("GetUsers: started");
      var vm = this;
      fetch("https://localhost:44364/api/users")
        .then(response => response.json())
        .then(users => {
          vm.users = users;
          console.log("GetUsers: done");
        })
        .catch(function(error) {
          console.log("GetUsers: error: ") + error;
        });
    },
    getQuestions() {
      //need chek
      console.log("getQuestions: started");
      var vm = this;
      fetch("https://localhost:44364/api/question")
        .then(response => response.json())
        .then(questions => {
          vm.questions = questions;
          console.log("getQuestions: done");
        })
        .catch(function(error) {
          console.log("getQuestions: error: ") + error;
        });
    },
    addQuestion(question) {
      question.UserOwnerId = this.currentUser.userOwnerId;
      fetch("https://localhost:44364/api/question", {
        method: "POST",
        headers: {
          "Content-Type": "application/json;charset=utf-8"
        },
        body: JSON.stringify(question)
      })
        .then(response => response.json())
        .then(result => {
          console.log("response: " + result);
        })
        .catch(function(error) {
          console.log("Ошибка! Не могу связаться с API. " + error);
        });
    },
    addUser() {
      //need chek
      if (this.nickname.trim() === "" || this.email.trim() === "") {
        this.answer = "there are no content!!!";
        return;
      }

      const user = {
        nickName: this.nickname,
        email: this.email
      };

      fetch("https://localhost:44364/api/users", {
        method: "POST",
        headers: {
          "Content-Type": "application/json;charset=utf-8"
        },
        body: JSON.stringify(user)
      })
        .then(response => response.json())
        .then(result => {
          this.answer = "response: " + result;
        })
        .catch(function(error) {
          this.answer = "Ошибка! Не могу связаться с API. " + error;
        });
      this.nickname = "";
      this.email = "";
    }
  }
};
</script>

<style scoped>
.content {
  display: flex;
  flex-direction: column;
  align-content: center;
  margin-left: auto;
  margin-right: auto;
  width: 700px;

  background-color: rgb(166, 219, 150);
}
.home-container {
  display: flex;
  flex-direction: column;
}
</style>
