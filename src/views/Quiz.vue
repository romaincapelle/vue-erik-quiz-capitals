<template>
  <div class="container mx-auto text-2xl py-8 max-w-xl">
    <h1 class="py-8 text-center text-white text-4xl">
      Quiz 20 Questions
    </h1>
    <transition name="fade">
      <div v-if="!gameFinished">
        <transition name="component-fade" mode="out-in">
          <Question>
            <h3 class="text-gray-400 p-2  mb-3 text-lg">
              What is the capital of
              <span class="font-bold text-white">{{
                countryQuestionCountry
              }}</span>
              ?
            </h3>
          </Question>
        </transition>
        <Answers>
          <div>
            <div
              class="text-white text-lg p-2 border border-white mb-3 hover:bg-white hover:text-indigo-900 cursor-pointer"
              v-for="answer in mixedUpAnswers"
              :key="answer"
              @click="checkAnswer(answer)"
            >
              <p>{{ answer }}</p>
            </div>
          </div>
        </Answers>
        <div class="bg-black">
          <div class="progress-bar bg-teal-300" :style="progressBarStyle"></div>
        </div>

        <p class="text-white my-12">Score is {{ Score }}/{{ Index }}</p>
        <transition name="fade">
          <div
            class="p-3 border border-white border-double bg-gray-100"
            v-if="winningStrike >= 4"
            key="1"
          >
            <p class="text-5xl text-center text-teal-500">
              So Impressive !
            </p>
          </div>

          <div
            class="p-3 border border-white border-double bg-gray-100"
            v-else-if="winningStrike >= 2"
            key="2"
          >
            <p class="text-5xl text-center text-teal-300">
              Winning strike !
            </p>
          </div>

          <div v-else-if="winningStrike >= 1" key="3">
            <div class="p-3 border border-white border-double bg-gray-100">
              <p class="text-5xl text-center text-teal-300">
                Good
              </p>
            </div>
          </div>
        </transition>
      </div>
    </transition>
    <div v-if="gameFinished" class="border bg-white">
      <p v-if="Score <= 10" class="text-red-700 my-12 p-5 text-center">
        Not so great<br />
        Your Score is {{ Score }}/20
      </p>
      <p v-else-if="Score <= 15" class="text-white my-12">
        Pretty good<br />
        Your Score is {{ Score }}/20
      </p>
      <p v-else class="text-white my-12">
        Awesome<br />
        Your Score is {{ Score }}/20
      </p>
      <button
        @click="startOver"
        class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded"
      >
        Start Over
      </button>
    </div>
  </div>
</template>

<script>
import Question from '@/components/Question'
import Answers from '@/components/Answers'
import { Capitals } from '@/assets/capitals'

export default {
  data() {
    return {
      Capitals,
      Score: 0,
      Index: 0,
      loading: 0,
      wonThisQuestion: false,
      winningStrike: 0,
      countryQuestion: '',
      wrongAnswer01: '',
      wrongAnswer02: '',
      wrongAnswer03: '',
      gameFinished: false
    }
  },
  components: {
    Question,
    Answers
  },
  methods: {
    shuffleArray(a) {
      for (let i = a.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1))
        ;[a[i], a[j]] = [a[j], a[i]]
      }
      return a
    },
    checkAnswer(answer) {
      if (this.goodAnswer === answer) {
        this.Score++
        this.winningStrike++
        this.wonThisQuestion = true
        this.Index >= 20 ? (this.gameFinished = true) : this.newQuestion()
      } else {
        this.winningStrike = 0
        this.wonThisQuestion = false
        this.Index >= 20 ? (this.gameFinished = true) : this.newQuestion()
      }
    },
    newQuestion() {
      this.Index++
      this.newWrongAnswer01()
      this.newWrongAnswer02()
      this.newWrongAnswer03()
      this.createQuestion()
    },

    createQuestion: function() {
      var r00 = Math.floor(Math.random() * (this.countCountries - 0)) + 0
      this.countryQuestion = this.Capitals[r00]
    },

    newWrongAnswer01: function() {
      var r01 = Math.floor(Math.random() * (this.countCountries - 0)) + 0
      this.wrongAnswer01 = this.Capitals[r01].city
    },
    newWrongAnswer02: function() {
      var r02 = Math.floor(Math.random() * (this.countCountries - 0)) + 0
      this.wrongAnswer02 = this.Capitals[r02].city
    },
    newWrongAnswer03: function() {
      var r03 = Math.floor(Math.random() * (this.countCountries - 0)) + 0
      this.wrongAnswer03 = this.Capitals[r03].city
    },
    startOver: function() {
      this.gameFinished = false
      this.Index = 0
      this.Score = 0
      this.progressBarStyle = 0
      this.newWrongAnswer01()
      this.newWrongAnswer02()
      this.newWrongAnswer03()
      this.createQuestion()
    }
  },
  computed: {
    countCountries: function() {
      var countCountries = this.Capitals.length
      return countCountries
    },
    countryQuestionCountry: function() {
      var countryQuestionCountry = this.countryQuestion.country
      return countryQuestionCountry
    },
    goodAnswer: function() {
      var goodAnswer = this.countryQuestion.city
      return goodAnswer
    },
    mixedUpAnswers: function() {
      console.log('r01  is ' + this.wrongAnswer01)
      var mixedUpAnswers = []
      mixedUpAnswers.push(
        this.goodAnswer,
        this.wrongAnswer01,
        this.wrongAnswer02,
        this.wrongAnswer03
      )
      this.shuffleArray(mixedUpAnswers)
      return mixedUpAnswers
    },
    progressBarStyle: function() {
      return {
        width: this.Index * 5 - 5 + '%'
      }
    }
  },
  created() {
    this.newQuestion()
  }
}
</script>

<style>
.loading {
  max-width: 100%;
}
.progress-bar {
  color: #1e1d45;
  max-width: inherit;
  text-align: center;
  height: 10px;
  box-shadow: #81e6d9 0px 0px 7px;
}
.fade-enter-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
