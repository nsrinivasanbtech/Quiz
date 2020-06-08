<template>
  <div id="app" class="container-fluid">
    <!--<img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <b-container class="bv-example-row">
      <b-row>
        <b-col>
          <Header
            :numCorrect="numCorrect"
            :numTotal="numTotal"
          />
          <QuestionBox
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :questionLength="questionLength"
            :questionIndex="index"
            :next="next"
            :increment="increment"
          />
        </b-col>
      </b-row>
    </b-container>
    <div v-if="!questions.length"><Spinner/></div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
import Spinner from './components/Spinner.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox,
    Spinner
  },
  data(){
    return{
      questions: [],
      index: 0,
      questionLength: '',
      numCorrect: 0,
      numTotal: 0
    }
  },
  methods: {
    next() {
      this.index++;
    },
    increment(isCorrect){
      if(isCorrect){
        this.numCorrect++;
      }
      this.numTotal++;
    }
  },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=21&difficulty=easy&type=multiple',{
      method: 'get'
    })
    .then((response) => {
      return (response.json())
    })
    .then((jsonData) => {
      console.log(jsonData)
      this.questions = jsonData.results;
      this.questionLength = this.questions.length;
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
  margin: 60px 0px;
}
</style>
