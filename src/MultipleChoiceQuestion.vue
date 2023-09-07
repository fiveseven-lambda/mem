<script setup>
import { ref } from 'vue'

const emit = defineEmits(['check'])
const props = defineProps(['question', 'question_index'])

const selected = ref({})
</script>

<template>
  <template v-for="(choice, choice_index) in question.choices">
    <input
      type="checkbox"
      :name="question_index"
      :id="question_index + ':' + choice_index"
      @click="event => {
        selected[choice_index] = event.target.checked;
        emit('check', question.ans.every((ans, index) => (selected[index] ?? false) == ans))
      }"
    />
    <label :for="question_index + ':' + choice_index">{{ choice }}</label>
  </template>
</template>
  