<script setup>
import Search from "@/components/Search for.vue";
import window from "@/components/window.vue";
import {ref} from "vue";
const Create = ref(false);

function StartAsk(){
  Create.value = !Create.value;
}
</script>

<template>
<div>

  <p class="title-text">
    FUNNY CAT
  </p>

  <p class="text-1">
    Get answer from your friends.
  </p>

  <Search class="search"></Search>

  <div class="wire"></div>

  <window  v-show="Create"></window>

  <button @click="StartAsk" type="button" class="Create-button" >
    <div class="Create-button-text" >
      Create
    </div>
    <!--    @click="emits('Create')"-->
  </button>





</div>
</template>

<style scoped>
.title-text{
    width: 3000px;
    height: 130px;
    background-image: linear-gradient(to right, #443D6B,#54CFC0);
    //-webkit-mask: linear-gradient(to right, #443D6B ,#54CFC0);
    -webkit-background-clip: text;
    color: transparent;
    font-size: 150px;
    font-style: normal;
    font-weight: 900;
    line-height: 90%;
    letter-spacing: 150px;
     word-spacing: 50px;
    margin-left: 3rem;
    margin-top: 1rem;
}
.text-1{
  width: 3000px;
  height: 130px;
  color: #54CFC0;
  font-size: 70px;
  word-spacing: 50px;
  letter-spacing: 15px;
  margin-left:35rem;
  margin-top: 3rem;
}

.Create-button {
  width: 250px;
  height: 70px;
  flex-shrink: 0;
  border-radius: 25px;
  background: #443D6B;
  box-shadow: 4px 4px 4px 0px rgba(0, 0, 0, 0.25);
  margin-left: 120rem;
  margin-top: 15rem;
  border: 0;
  outline: none;
}

.Create-button:hover{
  box-shadow: none;
}
.Create-button:active {
  box-shadow: inset 4px 4px 4px 0 rgba(0, 0, 0, 0.25);
}

.Create-button-text{
  color: #181818;
  font-size: 36px;
  font-style: normal;
  font-weight: 700;
  line-height: normal;
}

.search{
  margin-left: 12rem;
  margin-top: 3rem;

}

.wire{
  width: 75vw;
  height: 3px;
  background: #443D6B;
  margin-left: 15rem;
  margin-top: 8rem;
}


</style>