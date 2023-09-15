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

const antibiotic_mechanism = ['細胞壁合成阻害', 'タンパク質合成阻害', '核酸合成阻害', '葉酸代謝阻害']
const incubation_periods = ['2〜3時間', '1〜3日', '2〜3週間', '数年']
const virus_class = ['2本鎖DNA', '1本鎖DNA', '2本鎖RNA', '1本鎖RNA']
const parasite_oral_infection = ['豚肉', '牛肉', 'アジ・サバ', 'サケ・マス', 'アユ', 'タニシ・コイ', 'サワガニ', '有機野菜']

const questions = _.shuffle([create_multiple(
  'アミノグリコシド系を全て選べ',
  ['ゲンタマイシン', 'カナマイシン', 'ストレプトマイシン'], 2,
  ['エリスロマイシン', 'クラリスロマイシン', 'アジスロマイシン', 'バンコマイシン', 'ホスホマイシン'], 3
), create_multiple(
  'マクロライド系を全て選べ',
  ['エリスロマイシン', 'クラリスロマイシン', 'アジスロマイシン'], 2,
  ['ゲンタマイシン', 'カナマイシン', 'ストレプトマイシン', 'バンコマイシン', 'ホスホマイシン'], 3
), {
  text: 'ペニシリン系の作用機序は',
  choices: antibiotic_mechanism,
  ans: 0,
}, {
  text: 'セフェム系の作用機序は',
  choices: antibiotic_mechanism,
  ans: 0,
}, {
  text: 'アミノグリコシド系の作用機序は',
  choices: antibiotic_mechanism,
  ans: 1,
}, {
  text: 'マクロライド系の作用機序は',
  choices: antibiotic_mechanism,
  ans: 1,
}, {
  text: 'テトラサイクリン系の作用機序は',
  choices: antibiotic_mechanism,
  ans: 1,
}, {
  text: 'キノロン系の作用機序は',
  choices: antibiotic_mechanism,
  ans: 2,
}, {
  text: 'サルファ剤の作用機序は',
  choices: antibiotic_mechanism,
  ans: 3,
}, {
  text: 'ブドウ球菌は',
  choices: ['グラム陽性', 'グラム陰性'],
  ans: 0,
}, {
  text: '黄色ブドウ球菌食中毒の潜伏期間は',
  choices: incubation_periods,
  ans: 0,
}, create_multiple(
  '黄色ブドウ球菌感染症の症状',
  ['せつ', 'よう', '蜂窩織炎', '心内膜炎', '骨髄炎', '髄膜炎', '膿痂疹'], 4,
  ['丹毒'], 1
), create_multiple(
  'MRSA感染症の治療薬',
  ['バンコマイシン'], 1,
  ['ペニシリン', 'メチシリン', 'エリスロマイシン', 'テトラサイクリン'], 3
), {
  text: 'レンサ球菌は',
  choices: ['グラム陽性', 'グラム陰性'],
  ans: 0,
}, create_multiple(
  '溶連菌感染症の症状',
  ['咽頭炎', '扁桃炎', '膿痂疹', 'いちご舌', '口囲蒼白', '丹毒', '蜂窩織炎'], 4,
  [], 0
), create_multiple(
  '溶連菌感染後の続発症',
  ['リウマチ熱', '急性糸球体腎炎'], 2,
  ['白内障'], 1
), {
  text: '溶連菌に対する第一選択薬',
  choices: ['ペニシリン系', 'アミノグリコシド系', 'マクロライド系'],
  ans: 0
}, {
  text: '肺炎球菌は',
  choices: ['グラム陽性', 'グラム陰性'],
  ans: 0,
}, create_multiple(
  '肺炎球菌感染症の症状',
  ['肺炎', '髄膜炎'], 2,
  ['膿痂疹', '心内膜炎'], 2
), create_multiple(
  '芽胞を形成するのは',
  ['破傷風菌', 'ボツリヌス菌', 'ウェルシュ菌', 'ディフィシル菌'], 3,
  ['緑膿菌', 'レジオネラ菌'], 1
), {
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
}, {
  text: '淋菌は',
  choices: ['グラム陽性', 'グラム陰性'],
  ans: 1,
}, {
  text: '髄膜炎菌は',
  choices: ['グラム陽性', 'グラム陰性'],
  ans: 1,
}, create_multiple(
  '結核の治療薬',
  ['イソニアジド', 'リファンピシン', 'ピラジナミド'], 3,
  ['テトラサイクリン', 'ペニシリン', 'バンコマイシン', 'エリスロマイシン'], 2
), create_multiple(
  'マイコプラズマに対する第一選択薬',
  ['マクロライド系'], 1,
  ['ペニシリン系', 'セフェム系', 'グリコペプチド系', 'アミノグリコシド系'], 3
), {
  text: 'ヘルペスウイルスは',
  choices: virus_class,
  ans: 0,
}, create_multiple(
  '先天性サイトメガロウイルス感染症の症状',
  ['小頭症', '肝脾腫'], 2,
  [], 0
), {
  text: 'パルボウイルスは',
  choices: virus_class,
  ans: 1,
}, {
  text: 'A型肝炎ウイルスは',
  choices: virus_class,
  ans: 3,
}, {
  text: '風疹ウイルスは',
  choices: virus_class,
  ans: 3,
}, create_multiple(
  '先天性風疹症候群の症状',
  ['難聴', '心奇形', '白内障'], 3,
  [], 0
), {
  text: 'C型肝炎ウイルスは',
  choices: virus_class,
  ans: 3,
}, {
  text: 'インフルエンザウイルスは',
  choices: virus_class,
  ans: 3,
}, {
  text: '麻疹ウイルスは',
  choices: virus_class,
  ans: 3,
}, create_multiple(
  '先天性トキソプラズマ症の症状',
  ['網膜脈絡炎', '水頭症', '脳内石灰化'], 3,
  [], 0
), {
  text: '有鉤条虫の感染源は',
  choices: parasite_oral_infection,
  ans: 0
}, {
  text: '無鉤条虫の感染源は',
  choices: parasite_oral_infection,
  ans: 1
}, {
  text: 'アニサキスの感染源は',
  choices: parasite_oral_infection,
  ans: 2
}, {
  text: '日本海裂頭条虫の感染源は',
  choices: parasite_oral_infection,
  ans: 3
}, {
  text: '横川吸虫の感染源は',
  choices: parasite_oral_infection,
  ans: 4
}, {
  text: '肝吸虫の感染源は',
  choices: parasite_oral_infection,
  ans: 5
}, {
  text: '宮崎肺吸虫の感染源は',
  choices: parasite_oral_infection,
  ans: 6
}, {
  text: 'ウェステルマン肺吸虫の感染源は',
  choices: parasite_oral_infection,
  ans: 6
}, {
  text: '回虫の感染源は',
  choices: parasite_oral_infection,
  ans: 7
}])

const number = ref(1)
const point = ref(0)
</script>

<template>
  <Question
    v-for="(question, index) in questions.slice(0, number)"
    :question="question"
    :question_index="index"
    :key="index"
    @next="diff => {
      point += diff;
      number = Math.max(number, index + 2)
    }"
  />
  <p> 正答率 {{ point }} / {{ number }} = {{ Math.round(point / number * 100) }} % </p>
</template>
