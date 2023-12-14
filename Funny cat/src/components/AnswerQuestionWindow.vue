<script setup>
import {ref} from "vue";
const show = ref(false);
const ChangeButton = ref("Show the Question");
const Answer_text = ref("")

import {QuestionResponse} from "@/Cache";
import QuestionSection from "@/components/QuestionSection.vue";
import axios from "axios";
import router from "@/router";

function showQuestion(){
 show.value=!show.value;
 if(show.value){
   ChangeButton.value="Hide the Question"
 }
 else{
   ChangeButton.value="Show the Question"
 }
}

function answer_button(){
  axios.post('/api/questions/'+QuestionResponse.value.id, {
    "answer": Answer_text.value,
    "username": localStorage.getItem("Username"),
    "password": localStorage.getItem("Password"),
  })
      .then(function (response) {
        console.log(response);
        QuestionResponse.value.answers.push (response.data);
      })
      .catch(function (error) {
        console.log(error);
      });
}



</script>

<template>

  <div>
    <button @click="showQuestion" class="show-question">
      {{ChangeButton}}
    </button>

    <QuestionSection v-show="show"></QuestionSection>


    <div>
      My answer is:
    </div>

    <textarea v-model="Answer_text">

    </textarea>

    <button @click="answer_button"  class="answer" >
      Answer
    </button>
  </div>

</template>

<style scoped>




</style>