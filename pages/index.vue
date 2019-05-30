<template>
  <section class="container">
    <div>
      {{questions}}
      <br>
      <a class="button is-primary is-rounded">TRUE</a>
      <a class="button is-danger is-rounded">FALSE</a>
    </div>
  </section>
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

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>

<script>
export default {
  components: {},

  data() {
    return {
      questions: []
    };
  },

  mounted() {
    this.$axios
      .get("https://opentdb.com/api.php?amount=10&type=boolean")
      .then(res => (this.questions = res.data.results[0].question));
  }
};
</script>
