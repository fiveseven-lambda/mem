<script setup>
import { ref } from 'vue'
import _ from 'lodash';
import Question from './Question.vue'

function create_multiple(
  text,
  correct_choices,
  num_correct_choices,
  wrong_choices,
  num_wrong_choices,
){
  const selected_correct_choices = _.shuffle(correct_choices).slice(0, num_correct_choices).map(choice => [choice, true])
  const selected_wrong_choices = _.shuffle(wrong_choices).slice(0, num_wrong_choices).map(choice => [choice, false])
  const selected_choices = _.shuffle(_.concat(selected_correct_choices, selected_wrong_choices))
  return {
    text: text,
    choices: selected_choices.map(([choice, _]) => choice),
    ans: selected_choices.map(([_, ans]) => ans),
  }
}

const questions = _.shuffle([{
  text: 'ボツリヌス菌は',
  choices: ['グラム陽性', 'グラム陰性'],
  ans: 0,
}, {
  text: 'ディフィシル菌は',
  choices: ['グラム陽性', 'グラム陰性'],
  ans: 0,
}, {
  text: 'レジオネラ菌は',
  choices: ['グラム陽性', 'グラム陰性'],
  ans: 1,
}, create_multiple(
  '結核の治療薬',
  ['イソニアジド', 'リファンピシン', 'ピラジナミド'], 3,
  ['テトラサイクリン', 'ペニシリン', 'バンコマイシン'], 2
), create_multiple(
  'マイコプラズマ肺炎の治療薬',
  ['アジスロマイシン'], 1,
  ['ペニシリン', 'カナマイシン', 'ストレプトマイシン', 'セファロスポリン'], 2
),
])

const number = ref(1)
</script>

<template>
  <Question
    v-for="(question, index) in questions.slice(0, number)"
    :question="question"
    :question_index="index"
    :key="index"
    @next="number = Math.max(number, index + 2)"
  />
</template>
