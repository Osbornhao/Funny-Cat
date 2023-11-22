<script setup>

</script>

<template>
<div class="window">

  <div class="text1">
    My question is:
  </div>

  <textarea name="textarea" rows="10" cols="50" class="text-area"></textarea>

<br>
  <button  type="button" class="ask-button">
    <div class="ask-button-text" >
      Ask
    </div>
    <!--    @click="emits('Create')"-->
  </button>


</div>
</template>

<style scoped>
.text1{
  font-size: 36px;
  font-style: normal;
  font-weight: 700;
}

.ask-button {
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

.ask-button:hover{
  box-shadow: none;
}
.ask-button:active {
  box-shadow: inset 4px 4px 4px 0 rgba(0, 0, 0, 0.25);
}

.ask-button-text{
  color: #181818;
  font-size: 36px;
  font-style: normal;
  font-weight: 700;
  line-height: normal;
}

.window{
  background: #323232a2;
  width: 100vw;
  height:100vh;
  position:absolute;
  left:0;
  top:0;
}

.text-area{
  width: 40vw;
  height: 3vh;
  margin-left: 30rem;
  margin-top: -3rem;
}
</style>