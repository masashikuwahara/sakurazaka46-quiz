<template>
<div  v-if="!quizStarted" >
  <h1 class="text-center">櫻坂46に関するクイズです</h1>
  <h2 class="text-center">ぜひ挑戦してみてください。</h2>
  <div class="d-grid gap-2 col-6 mx-auto">
    <button class="btn " @click="startQuiz">スタート！</button>
  </div>
</div>
<div v-else-if="!quizFinished">
  <h2 class="mb-4">{{ currentQuestion.id }}.{{ currentQuestion.question }}</h2>
  <img v-if="currentQuestion.question === 'この後どうなった？'" src="@/assets/000.jpg" alt="">
  <div class="btn-group d-grid gap-3">
    <button v-for="(option, index) in currentQuestion.options" :key="index" class="btn btn-outline-primary" @click="answerQuestion(option)">
      {{ option }}
    </button>
  </div>
</div>
<div v-else>
  <h2 class="mb-4">クイズ結果</h2>
  <table class="table">
      <thead>
        <tr>
          <th>問題</th>
          <th>正解</th>
          <th>回答</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(question, index) in questions" :key="index">
          <td>{{ question.question }}</td>
          <td>{{ question.answer }}</td>
          <td v-if="userAnswers[index] === question.answer">&#x2713;</td>
          <td v-else>&#x2717;</td>
        </tr>
      </tbody>
    </table>
    <p v-if="correctAnswers >= 8" class="text-primary display-2">あなたは上級Buddies！</p>
    <p v-else-if="correctAnswers >= 5 && correctAnswers <= 7" class="text-primary display-2">あなたはなかなかのBuddies！</p>
    <p v-else class="text-danger display-2">もう少し頑張りましょう</p>
    <p>{{ correctAnswers }}/10 問正解</p>
    <button class="btn btn-primary" @click="restartQuiz">スタート画面へもどる</button>
</div>
</template>

<script>
export default {
  data() {
    return {
      quizStarted: false,
      quizFinished: false,
      currentQuestionIndex: 0,
      correctAnswers: 0,
      questions: [
        { id: 1, question: "楽屋で椅子に頭が挟まって抜けなくなったメンバーは？", options: ["井上梨名", "増本綺良", "松田里奈", "大沼晶保"], answer: "増本綺良" },
        { id: 2, question: "2024年1月8日OAそこ曲がったら、櫻坂？で小田倉麗奈が澤部におねだりしたものは？", options: ["クルーザー", "レクサス", "オーデマピゲの時計", "ゴルフ場"], answer: "ゴルフ場" },
        { id: 3, question: "森田ひかるが3年以上行ってない場所は？", options: ["美容室", "コンビニ", "ディズニーシー", "ドン・キホーテ"], answer: "美容室" },
        { id: 4, question: "山下瞳月の好きな色は？", options: ["パステルブルー", "ターコイズ", "オレンジ", "ピンク"], answer: "ピンク" },
        { id: 5, question: "2021年5月2日OAそこ曲がったら、櫻坂？で藤吉夏鈴の家のテレビの大きさが暴露されたがどのくらいの大きさと言われたか？", options: ["スマホサイズ", "パソコンのモニターくらい", "カーナビサイズ", "90インチ"], answer: "カーナビサイズ" },
        { id: 6, question: "大沼晶保の得意技は？", options: ["跳び蹴り", "右ストレート", "背負い投げ", "チョーク"], answer: "跳び蹴り" },
        { id: 7, question: "山﨑天の嫌いな動物は？", options: ["子犬", "小動物", "爬虫類", "小鳥"], answer: "小動物" },
        { id: 8, question: "谷口愛季は活舌が悪いが特に何行が苦手？", options: ["ア行とサ行", "カ行とハ行", "タ行とラ行", "ナ行とマ行"], answer: "タ行とラ行" },
        { id: 9, question: "この後どうなった？", imagePath: require('@/assets/000.jpg').default, options: ["上手くキャッチした", "ボールをうまく投げられなかった", "前転すらもできなかった", "顔面にボールをぶつけて悶絶"], answer: "顔面にボールをぶつけて悶絶" },
        { id: 10, question: "田村保乃が自分を好きだと言ってくれるメンバーで結成したグループのメンバーは石森璃花、山下瞳月とあと一人は？", options: ["遠藤理子", "的野美青", "村井優", "小島凪紗"], answer: "小島凪紗" },
      ],
      userAnswers: []
    }
  },
  computed: {
    currentQuestion() {
      return this.questions[this.currentQuestionIndex];
    }
  },
  methods: {
    startQuiz() {
      this.quizStarted = true;
    },
    answerQuestion(option) {
      this.userAnswers.push(option);
      if (option === this.currentQuestion.answer) {
        this.correctAnswers++;
      }
      if (this.currentQuestionIndex < this.questions.length - 1) {
        this.currentQuestionIndex++;
      } else {
        this.quizFinished = true;
      }
    },
    restartQuiz() {
      this.quizStarted = false;
      this.quizFinished = false;
      this.currentQuestionIndex = 0;
      this.correctAnswers = 0;
      this.userAnswers = [];
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

img {
  width: 100%;
}

.btn {
  background-color: #f19db5;
}

.btn:hover {
  background-color: #f19db5b0;
}
</style>
