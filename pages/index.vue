<template>
  <section class="container">
    <div>
      <h1 class="title">
        time-out-trivia
      </h1>
      <h2 class="subtitle">
        Simple Yes-No answer trivia web-app (school project)
      </h2>
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
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
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
      questions : []
    }
  },

  mounted(){
    this.$axios.get('https://opentdb.com/api.php?amount=10&type=boolean')
    .then(res => 
    this.questions = res
    )
  }
}
</script>
