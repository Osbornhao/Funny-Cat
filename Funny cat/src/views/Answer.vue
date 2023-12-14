<script setup>
import md5 from 'js-md5';
import {QuestionResponse} from '@/Cache'
import axios from "axios";
import router from "@/router";
console.log(QuestionResponse)

import AnswerQuestionWindow from "@/components/AnswerQuestionWindow.vue";

import {ref} from "vue";
import QuestionSection from "@/components/QuestionSection.vue";
const Username = ref();
const Password =ref();
const Answer =ref();
const Enter =ref();
const ChangeAnswer = ref("My answer is:");
const logined =ref(false);
const AqwShow = ref(false);

function moveFocus(){
  Enter.value.focus()
}
function text1(){
  alert(md5('Message to hash'))
  console.log(md5('Message to hash'))
  let hashedPassword = md5(Password.value)
  localStorage.setItem("Username",Username.value)
  localStorage.setItem("Password",hashedPassword)
  let tokenPassword = md5(Username.value+hashedPassword)
  for (var i=0;i<QuestionResponse.value.answers.length;i++)
  {
    if (QuestionResponse.value.answers[i].access_token === tokenPassword){
        logined.value = true;
        ChangeAnswer.value = "Update your answer";
        return;
    }
  }
  logined.value= true;
}

function postUserAnswer(){
  axios.post('/api/questions/'+QuestionResponse.id, {
    "username": Username.value,
    "password": Password.value,
    "answer": Answer.value
  })
      .then(function (response) {
        console.log(response);
        console.log(response.data);
        QuestionResponse.value = response.data;
        router.push('/Answer');
      })
      .catch(function (error) {
        console.log(error);
      });
}

function logout(){
  localStorage.removeItem("Username")
  localStorage.removeItem("Password")
  logined.value= false;
}

function answerQuestion(){
  AqwShow.value=!AqwShow.value;
}



</script>

<template>
  <div class="grid">

    <p class="title-text1">
      FUNNY CAT
    </p>
    <div class="search-input">search</div>

    <QuestionSection>
    </QuestionSection>

    <div class="text-answer">
      <div v-for="answer_element in QuestionResponse.answers">
        <h2>{{answer_element.by}}({{answer_element.id}}):</h2>
        <p>{{answer_element.answer}}</p>
        <p>-- last updated at {{answer_element.last_updated}}</p>
      </div>
    </div>

    <div class="wire2"></div>

    <div class="login" v-if="!logined">
      <p class="title-text2">
      Login
      </p>

      <input @keyup.enter="moveFocus"  class="login-text" type="text" v-model="Username"/>

      <input ref="Enter"  @keyup.enter="text1"   class="password"  type="password"  v-model="Password"/>
      <button @click="text1" type="button" class="login-button" >
        login
      </button>
    </div>

    <div class="login" v-if="logined">
      <p class="title-text2">
        Hi,{{Username}}
      </p>
      <AnswerQuestionWindow v-show="AqwShow"></AnswerQuestionWindow>
      <button @click="answerQuestion" type="button" class="login-button" >
        {{ChangeAnswer}}
      </button>
      <button  @click="logout" type="button" class="logout-button">
        Logout
      </button>
    </div>
  </div>
</template>

<style scoped>
.grid{
  display: grid;
  grid-template-rows: 100px 2fr 4fr;
  grid-template-columns: 1.5fr 1fr;
  height: 100%;
}


.title-text1{
  //width: 40vw;
  //height: 10vh;
  font-size: 100px;
  font-style: normal;
  font-weight: 300;
  letter-spacing: 5px;
  word-spacing: 5px;
  margin-left: 0;
  margin-top: -2rem;
  background-image: linear-gradient(to right, #443D6B,#54CFC0);
//-webkit-mask: linear-gradient(to right, #443D6B ,#54CFC0);
  -webkit-background-clip: text;
  color: transparent;

}
.text-question{
  margin-left: 0;
  margin-top: 0;
}
.text-answer{
  margin-left:0;
  margin-top: 0;
}
.login{
  margin-left: 0;
  margin-top: 0;
  grid-column-start: 2;
  grid-row-start:2;
  grid-row-end: 4;
}
.title-text2{
  font-size: 50px;
  font-style: normal;
  font-weight: 400;
}
.login-text{
  width: 3vw;
  height: 5vh;
}
.wire2{
  position: absolute;
}

</style>