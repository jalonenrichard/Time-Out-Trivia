<template id="question-template">
  <div id="whole-page-div">
    <section class="container" id="question-section">
      <div id="question-div">
        <div id="score-counter">SCORE: {{score}}</div>
        <div id="question-div-content">
          <b-spinner v-if="isLoading" label="Loading..." id="loading-spinner"></b-spinner>
          <div v-else>
            <br>
            <p v-html="question_data.question"></p>
            <br>
            <div v-if="isGameOver">
              <a class="button is-primary is-rounded" v-on:click="startNewGame()">New Game</a>
            </div>
            <div v-else id="buttons-div">
              <a class="button is-primary is-rounded" v-on:click="checkAnswer('True')">TRUE</a>
              <a class="button is-danger is-rounded" v-on:click="checkAnswer('False')">FALSE</a>
            </div>
          </div>
        </div>
      </div>
    </section>
    <b-modal v-model="showModal" centered title="Whoops!" ok-title="New Game" ok-only>
      Answer '
      <span id="wrong-answer">{{wrongAnswer}}</span>' was wrong to question:
      <p v-html="question_data.question"></p>Game Over!
      <br>
      Total Score: {{score}}
      <template slot="modal-footer" slot-scope="{ ok }">
        <!-- Emulate built in modal footer ok and cancel button actions -->
        <b-button size="sm" variant="success" @click="ok();startNewGame()">New Game</b-button>
      </template>
    </b-modal>
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
  min-height: 20em;
  min-width: 100%;
  color: white;
  padding: 5em;
  background: rgba(0, 0, 0, 0.5);
}

#question-div-content {
  margin-top: 2em;
}

#whole-page-div {
  background-image: url("../static/q-mark.jpg");
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

#score-counter {
  margin-bottom: 2em;
  width: 8em;
  position: absolute;
  margin-left: auto;
  margin-right: auto;
  left: 0;
  right: 0;
  border: 1px solid rgb(77, 77, 77);
  border-radius: 10px;
}

#loading-spinner {
  margin-top: 2em;
}

#wrong-answer {
  color: red;
}
</style>

<script>
export default {
  components: {},

  data() {
    return {
      question_data: "",
      score: 0,
      isLoading: false,
      showModal: false,
      isGameOver: false,
      wrongAnswer: ""
    };
  },
  beforeMount() {
    this.isLoading = true;
  },
  mounted() {
    this.apiCall();
  },

  methods: {
    checkAnswer: function(answer) {
      if (this.question_data.correct_answer == answer) {
        this.isLoading = true;
        this.score++;
        this.apiCall();
      } else {
        this.wrongAnswer = answer;
        this.gameOver();
      }
    },
    apiCall: function() {
      this.$axios
        .get("https://opentdb.com/api.php?amount=1&type=boolean")
        .then(
          res => (
            (this.question_data = res.data.results[0]), (this.isLoading = false)
          )
        );
    },
    gameOver: function() {
      this.isGameOver = true;
      this.showModal = true;
    },
    startNewGame: function() {
      this.score = 0;
      this.isGameOver = false;
      this.isLoading = true;
      this.apiCall();
    }
  }
};
</script>
