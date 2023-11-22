<script setup>
import router from "@/router";
function answer(){
  router.push('/Answer')

}

</script>

<template>
<div>
  <p class="text-1">
    Let's check question id:
  </p>

  <input type="text" class="input"/>

  <br>
  <button @click="answer" type="button" class="take-button">
    <div class="take-button-text" >
      Take me
    </div>
    <!--    @click="emits('Create')"-->
  </button>



</div>
</template>

<style scoped>
.text-1{
  font-size: 36px;
  font-style: normal;
  font-weight: 700;
}

.take-button {
  width: 250px;
  height: 70px;
  flex-shrink: 0;
  border-radius: 25px;
  background: #443D6B;
  box-shadow: 4px 4px 4px 0px rgba(0, 0, 0, 0.25);
  margin-left: 30rem;
  margin-top: 20rem;
  border: 0;
  outline: none;
}

.take-button:hover{
  box-shadow: none;
}
.take-button:active {
  box-shadow: inset 4px 4px 4px 0 rgba(0, 0, 0, 0.25);
}

.take-button-text{
  color: #181818;
  font-size: 36px;
  font-style: normal;
  font-weight: 700;
  line-height: normal;
}

.input{
  width: 40vw;
  height: 3vh;
  margin-left: 30rem;
  margin-top: -3rem;
}






</style>