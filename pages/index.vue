<template id="question-template">
  <div id="whole-page-div">
    <section class="container" id="question-section">
      <div id="question-div">
        <div>
          <div id="score-counter">SCORE: {{score}}</div>
          <br>
          <p v-html="question_data.question"></p>
          <br>
          <div id="buttons-div">
            <a class="button is-primary is-rounded" v-on:click="checkAnswer('True')">TRUE</a>
            <a class="button is-danger is-rounded" v-on:click="checkAnswer('False')">FALSE</a>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

#question-div {
  min-width: 40em;
  color: white;
  padding: 5em;
  background: rgba(0, 0, 0, 0.5);
}

#buttons-div {
  margin-top: 2em;
}

#whole-page-div {
  background-image: url("../static/q-mark.jpg");
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

#score-counter {
  margin-bottom: 2em;
  border: 1px solid rgb(77, 77, 77);
  border-radius: 5px;
  padding-right: 1em;
}
</style>

<script>
export default {
  components: {},

  data() {
    return {
      question_data: "",
      score: 0
    };
  },

  mounted() {
    this.apiCall();
  },

  methods: {
    checkAnswer: function(answer) {
      if (this.question_data.correct_answer == answer) {
        this.score++;
        this.apiCall();
      }
    },
    apiCall: function() {
      this.$axios
        .get("https://opentdb.com/api.php?amount=1&type=boolean")
        .then(res => (this.question_data = res.data.results[0]));
    }
  }
};
</script>
