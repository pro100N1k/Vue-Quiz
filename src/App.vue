<template>
  <div id="app">
<!--    <img alt="Vue logo" src="./assets/logo.png">-->
<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <Header
        :numCorrect="numCorrect"
        :numTotal="numTotal"
        :numCurrent = "numCurrent"
    />
      <b-container>
          <b-row>
              <b-col sm="6" offset="3">
                  <QuestionBox
                     v-if="questions.length"
                    :currentQuestion="questions[index]"
                    :next="next"
                     :increment="increment"
                  />
              </b-col>
          </b-row>
      </b-container>
  </div>
</template>

<script>
import Header from "./components/Header";
import QuestionBox from "./components/QuestionBox";

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox
  },
    data() {
      return {
        questions: [],
        index: 0,
        numCurrent: 0,
        numCorrect: 0,
        numTotal: 0
      }
    },
    methods: {
      next() {
          this.index++
      },
        increment(isCorrect) {
          if(isCorrect) {
              this.numCorrect++
          }
          this.numCurrent++
        }
    },
    mounted: function() {
      fetch('https://opentdb.com/api.php?amount=10&category=11&difficulty=easy&type=multiple', {
          method: 'get'
      })
        .then((response) => {
            return response.json();
        })
        .then((jsonData) => {
            this.questions = jsonData.results
            this.numTotal = this.questions.length
        })
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
</style>
