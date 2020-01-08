<template>
  <div id="app">
    <Header :numTotal="numTotal" :total="questions.length" />

    <b-container class="box">
      <b-row>
        <b-col sm="12" offset="0">
          <QuestionBox
            v-if="questions.length && index < questions.length"
            :CurrQuestion="questions[index]"
            :next="next"
            :increment="increment"
          />
        </b-col>
        <b-col sm="6" offset="3" v-if="displayResults && index >= questions.length">
          <Results :numCorrect="numCorrect" :numTotal="numTotal" />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";
import Results from "./components/Results.vue";

export default {
  name: "app",
  components: {
    Header,
    QuestionBox,
    Results
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      displayResults: false
    };
  },
  methods: {
    next: function() {
      this.index++;
      this.numTotal++;
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++;
      }
    }
  },
  mounted: function() {
    fetch("https://opentdb.com/api.php?amount=10&category=22&type=multiple", {
      method: "get"
    })
      .then(response => {
        return response.json();
      })
      .then(jsonData => {
        this.questions = jsonData.results;
      });
      setInterval(() => this.displayResults = !this.visible, 1000)
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.box {
  margin-top: 10px;
}
</style>
