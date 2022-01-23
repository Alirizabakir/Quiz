<template>
  <div class="quizContainer w-112 h-98">
    <transition-group
      tag="div"
      mode="ease"
      enter-active-class="animate__animated animate__slideInRight"
      enter-leave-class="animate__animated animate__slideInRight"
      class="animate relative"
    >
      <div
        v-show="quiz.number == showData"
        v-for="quiz in quizData"
        :key="quiz"
        class="quizHeader absolute inset-0"
      >
        <div class="questionBox">
          <h2 class="question">{{ quiz.question }}</h2>
          <div class="flex items-center justify-center">
            <img
              class="w-4 h-4 opacity-60 mr-2"
              src="https://cdn-icons-png.flaticon.com/512/2910/2910890.png"
              alt=""
            />
            <p class="subQuestion">{{ quiz.subtext }}</p>
            
          </div>
        </div>
        <ul class="answerBox">
          <li v-for="item in quiz.answer" :key="item" class="answer">
            <input
              type="radio"
              :id="item.name"
              :value="item.name"
              v-model="resultData"
              name="answer"
              class="mr-2"
            />
            <label :for="item.name" class="answerLabel xxx">
              {{ item.text }}
            </label>
          </li>
        </ul>
        <button
          class="btn"
          @click="scoreEvent(quiz.result), showEvent(quiz.number)"
        >
          Next Question
        </button>
      </div>
      <transition
        tag="div"
        mode="ease-in"
        enter-active-class="animate__animated animate__slideInRight"
        enter-leave-class="animate__animated animate__slideInRight"
        class="animate relative"
      >
        <div
          v-show="showData == 'result'"
          class="resultHeader absolute inset-0"
        >
          <div class="resultBox">
            <h1 class="resultText">
              Qongratulations . You have completed the exam !
            </h1>
            <h1 class="scoreText">Score : {{ score }}/{{ quizData.length }}</h1>
            <div
              class="degreeBox"
              v-show="stats.value.find((a) => a == score) === score"
              v-for="stats in resultShow.degree"
              :key="stats"
            >
              <h2 class="degree">Degree : {{ stats.status }}</h2>
              <img :src="stats.emojiURL" class="emoji" />
            </div>
            <div class="btnBox">
              <button class="btnTry" @click="reset()">Try Again</button>
            </div>
          </div>
        </div>
      </transition>
    </transition-group>
  </div>
  <router-view />
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      score: 0,
      showData: 0,
      resultData: "",
      quizData: [
        {
          number: 0,
          result: "d_1",
          question: "Who conquered Istanbul ?",
          subtext: "He is the Ottoman Sultan !",
          answer: [
            {
              name: "a_1",
              text: "Yıldırım Bayezid",
              key: true,
            },
            {
              name: "b_1",
              text: "Osman Gazi",
              key: true,
            },
            {
              name: "c_1",
              text: "I. Murad",
              key: true,
            },
            {
              name: "d_1",
              text: "Fatih Sultan Mehmed",
              key: true,
            },
          ],
        },
        {
          number: 1,
          result: "c_2",
          question: "The capital city of Turkey is ...... ?",
          subtext: "La Bebe !",
          answer: [
            {
              name: "a_2",
              text: "Istanbul",
              key: true,
            },
            {
              name: "b_2",
              text: "KahramanMaraş",
              key: true,
            },
            {
              name: "c_2",
              text: "Ankara",
              key: true,
            },
            {
              name: "d_2",
              text: "Izmir",
              key: true,
            },
          ],
        },
        {
          number: 2,
          result: "b_3",
          question: "Which is a natural number ?",
          subtext: "Good Luck !",
          answer: [
            {
              name: "a_3",
              text: "-1",
              key: true,
            },
            {
              name: "b_3",
              text: "0",
              key: true,
            },
            {
              name: "c_3",
              text: "1/2",
              key: true,
            },
            {
              name: "d_3",
              text: "3,5",
              key: true,
            },
          ],
        },
        {
          number: 3,
          result: "c_4",
          question: "Which animal is not a mammal ?",
          subtext: "Where is the egg ?",
          answer: [
            {
              name: "a_4",
              text: "Bat",
              key: true,
            },
            {
              name: "b_4",
              text: "Dolphin",
              key: true,
            },
            {
              name: "c_4",
              text: "Penguin",
              key: true,
            },
            {
              name: "d_4",
              text: "Cow",
              key: true,
            },
          ],
        },
        {
          number: 4,
          result: "a_5",
          question: "Who wrote the 'İstiklal Marşı' ?",
          subtext: "He is a writer.",
          answer: [
            {
              name: "a_5",
              text: "Mehmet Akif Ersoy",
              key: true,
            },
            {
              name: "b_5",
              text: "Cemal SÜREYYA",
              key: true,
            },
            {
              name: "c_5",
              text: "Ali Rıza BAKIR",
              key: true,
            },
            {
              name: "d_5",
              text: "Unknown",
              key: true,
            },
          ],
        },
      ],
      resultShow: {
        degree: [
          {
            value: [5],
            status: "Awesome",
            emojiURL: "https://img.icons8.com/emoji/344/star-struck.png",
          },
          {
            value: [3, 4],
            status: "Great",
            emojiURL:
              "https://img.icons8.com/emoji/344/smiling-face-with-sunglasses.png",
          },
          {
            value: [1, 2],
            status: "Medium",
            emojiURL:
              "https://img.icons8.com/emoji/344/smiling-face-with-smiling-eyes.png",
          },
          {
            value: [0],
            status: "Try Again",
            emojiURL: "https://img.icons8.com/emoji/344/flushed-face.png",
          },
        ],
      },
    };
  },
  methods: {
    scoreEvent(score) {
      if (this.resultData == score) {
        this.score++;
      }
    },
    showEvent(index) {
      if (index + 1 < this.quizData.length) {
        this.showData++;
      } else {
        this.showData = "result";
      }
    },
    reset() {
      this.showData = 0;
      this.score = 0;
      this.resultData = "";
    },
  },
};
</script>

<style lang="scss">
#app {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgb(154, 237, 237);
}
</style>
