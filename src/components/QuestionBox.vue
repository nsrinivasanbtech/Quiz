<template>
    <div>
        <!-- <b-jumbotron fluid bg-variant="white" text-variant="white" border-variant="dark"> -->
            <b-row no-gutters class="main-question-container">    
                <b-col class="white">
                    <template slot:lead>
                        <div>
                            <div class="question-count">
                                <p class="title">
                                    <span class="question">Question {{ questionIndex + 1 }} / {{ questionLength }}</span>
                                </p>
                                <p class="questionArrow">
                                    <span class="arrow right"></span>
                                </p>
                            </div>
                            <p class="questionText" v-html="currentQuestion.question"></p>
                        </div>
                    </template>
                </b-col>
                <b-col class="optionsList">
                    <div>
                        <p class="title additionaltitle mx-auto">
                        Select the answers below
                        </p>
                        <!-- <ul>
                            <li v-for="(answer, index) in answers" :key="index">{{ answer }}</li>
                        </ul> -->
                        <b-list-group class="anwerContainer">
                            <b-list-group-item 
                                class="answerOption"
                                @click.prevent="selectedAnswer(index)"
                                :class="answercolorClass(index)"
                                v-for="(answer, index) in shuffledAnswers" :key="index"
                                v-html="answer">
                            </b-list-group-item>
                        </b-list-group>
                    </div>
                    <hr class="my-4">
                    <b-button variant="primary" href="#" @click="submitAnswer" :disabled="this.selectedIndex == null || answered">Submit</b-button>
                    <b-button variant="success" href="#" @click="next" :disabled="enableNext">Next</b-button>
                </b-col>
            </b-row>
        <!-- </b-jumbotron> -->
    </div>
</template>

<script>
import _ from 'lodash';
    export default {
        props: {
            currentQuestion: Object,
            questionLength: [String, Number],
            questionIndex: [String, Number],
            next: Function,
            increment: Function
        },
        data() {
            return{
                selectedIndex: null,
                correctIndex: null,
                shuffledAnswers: [],
                answered: false,
                enableNext: true
            }
        },
        watch: {
            currentQuestion: {
                immediate: true,
                handler() {
                    this.selectedIndex = null;
                    this.shuffleAnswers();
                    this.answered = false;
                    this.enableNext = true;
                }
            }
        },
        methods:{
            selectedAnswer(index) {
                this.selectedIndex = index;
            },
            shuffleAnswers() {
                this.shuffledAnswers = _.shuffle(this.answers);
                this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer);
                return this.shuffledAnswers;
            },
            submitAnswer() {
                let isCorrect = false;
                if(this.selectedIndex === this.correctIndex){
                    isCorrect = true;
                }
                this.answered = true;
                this.questionIndex === 9 ? this.enableNext= true : this.enableNext= false 
                this.increment(isCorrect)
            },
            answercolorClass(index) {
                return !this.answered && this.selectedIndex === index ? 'selected' : 
                this.answered && this.correctIndex === index ? 'correct' : 
                this.answered && this.selectedIndex === index && this.correctIndex !== index ? 'incorrect' : ''
            }
        },
        computed: {
            answers() {
                let answers = [...this.currentQuestion.incorrect_answers]
                answers.push(this.currentQuestion.correct_answer)
                return answers
            }
        }
    }
</script>

<style>
    .main-question-container{height: 400px;}
    .optionsList{background-color: #f8e2d5;}
    .white{background-color: #7bc5ce;color: #000000;}
    .question-count{display: flex;justify-content: center;margin-top: 10px;}
    .title{border-bottom: 1px solid #de376f;padding-bottom:5px;color:#de376f;width:160px;}
    .questionArrow{margin-left: 50px;}
    .arrow{border:solid #de376f;padding:4px;border-width: 0 3px 3px 0;display: inline-block;}
    .right{transform: rotate(-45deg);-webkit-transform: rotate(-45deg);}
    .questionText{margin:100px 0px; color: #40332b;}
    .additionaltitle{width: 300px;margin-top: 10px;}
    .anwerContainer{align-items: center;}
    .answerOption{background-color: #f8e2d5;width: 80%;border:none;border-bottom: 1px solid rgba(0,0,0,.125);padding-bottom: 20px;}
    .answerOption:hover{background-color: #15e7ff;cursor: pointer;}
    .selected{background-color: #7bc5ce;}
    .correct{background-color: lightgreen;}
    .incorrect{background-color: red;}
    .btn{margin-right: 10px;}
</style>