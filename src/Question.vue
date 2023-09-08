<script setup>
import { ref } from 'vue'
import _ from 'lodash'

import SingleChoiceQuestion from './SingleChoiceQuestion.vue'
import MultipleChoiceQuestion from './MultipleChoiceQuestion.vue'

const emit = defineEmits(['next'])
const props = defineProps(['question', 'question_index'])
const correct = ref(false)
</script>

<template>
  <p>{{ question.text }}</p>
  <MultipleChoiceQuestion
    v-if="_.isArray(question.ans)"
    :question="question"
    :question_index="question_index"
    @check="b => {
      const diff = +b - +correct;
      correct = b;
      emit('next', diff)
    }"
  />
  <SingleChoiceQuestion
    v-else
    :question="question"
    :question_index="question_index"
    @check="b => {
      const diff = +b - +correct;
      correct = b;
      emit('next', diff)
    }"
  />
</template>

<style scoped>
p {
  background-color: v-bind("correct ? 'white' : 'orange'")
}
</style>