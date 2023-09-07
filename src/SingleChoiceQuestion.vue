<script setup>
const emit = defineEmits(['check'])
const props = defineProps(['question', 'question_index'])
</script>

<template>
  <template v-for="(choice, choice_index) in question.choices">
    <input
      type="radio"
      :name="question_index"
      :id="question_index + ':' + choice_index"
      @click="emit('check', choice_index == question.ans)"
    />
    <label :for="question_index + ':' + choice_index">{{ choice }}</label>
  </template>
</template>