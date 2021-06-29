<template>
  <div class="author">
    <div id="nav">
      <router-link to="/">Home</router-link>
    </div>
    <h1>{{ author }}</h1>
    <p class="quote" v-for="(x, index) in author_quotes" :key="index">
      {{ x.quoteText }}
    </p>
  </div>
</template>

<script>
export default {
  data () {
    return {
      author: '',
      author_quotes: []
    }
  },
  mounted () {
    this.author = this.$route.params.author.replace('_', ' ')
    fetch(`https://quote-garden.herokuapp.com/api/v3/quotes?author=${this.author}`)
      .then(res => res.json())
      .then(res => { this.author_quotes = [...res.data] })
  }

}
</script>
