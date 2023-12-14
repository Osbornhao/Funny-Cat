<script setup>
import {QuestionResponse} from "@/Cache";
</script>

<template>
  <div class="text-question">
    <h2>Question({{QuestionResponse.id}})</h2>
    <p>{{QuestionResponse.question}}</p>
  </div>
</template>

<style scoped>

</style>