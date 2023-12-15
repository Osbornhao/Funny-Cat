<script setup>
import {ref, watch} from "vue";
const show = ref(false);
const ChangeButton = ref("Show the Question");
const Answer_text = ref("")
const props = defineProps(['foo',"id"])//answer
let isOlderUser = true

import {QuestionResponse} from "@/Cache";
import QuestionSection from "@/components/QuestionSection.vue";
import axios from "axios";
import router from "@/router";

Answer_text.value = props.foo
if(Answer_text.value === ""){
  isOlderUser = false
}
// watch(props, (newValue, oldValue) => {
//       console.log(newValue)
//       Answer_text.value = newValue.foo
//     },
//     { deep: true }
// )
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
  let data={
    "answer": Answer_text.value,
    "username": localStorage.getItem("Username"),
    "password": localStorage.getItem("Password"),
  }

  if(isOlderUser){
    axios.put('/api/answers/'+props.id, data)
        .then(function (response) {
          console.log(response);
          for (var i=0;i<QuestionResponse.value.answers.length;i++)
          {
            if (props.id === QuestionResponse.value.answers[i].id){
              QuestionResponse.value.answers[i].answer = response.data.answer
              QuestionResponse.value.answers[i].last_updated = response.data.last_updated
              return;
            }
          }
        })
        .catch(function (error) {
          console.log(error);
        });
  }
  else {
    axios.post('/api/questions/'+QuestionResponse.value.id, data)
      .then(function (response) {
        console.log(response);
        QuestionResponse.value.answers.push (response.data);
      })
      .catch(function (error) {
        console.log(error);
      });
  }
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