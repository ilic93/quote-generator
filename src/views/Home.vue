<template>

  <div class="home">
    <header>
      <button class="btn" @click="fetchQuote()">
        random <i class="fas fa-sync"></i>
      </button>
    </header>

    <p class="quote">{{ quote }}</p>

    <router-link :to="`/${author.replace(' ', '_')}`">
      <div class="author-info">
      <div class="info">
        <h3>{{ author }}</h3>
        <p>{{ genre }}</p>
      </div>
      <div class="icon">
        <i class="fas fa-arrow-right fa-lg"></i>
      </div>
    </div>
    </router-link>

  </div>
</template>

<script>

export default {
  name: 'Home',
  data () {
    return {
      quoteObject: null,
      quote: '',
      author: '',
      genre: '',
      quote_url: 'https://quote-garden.herokuapp.com/api/v3/quotes'
    }
  },
  methods: {
    fetchQuote () {
      fetch(`${this.quote_url}/random`)
        .then(res => res.json())
        .then(res => { this.quoteObject = res.data[0] })
    }
  },
  watch: {
    quoteObject () {
      this.quote = this.quoteObject.quoteText
      this.author = this.quoteObject.quoteAuthor
      this.genre = this.quoteObject.quoteGenre
    }
  },
  mounted () {
    this.fetchQuote()
  }
}
</script>

<style>

header {
  height: 50px;
}

.btn {
  border: none;
  background: white;
  float: right;
  font-size: 20px;
}

.btn:hover {
  cursor: pointer;
  box-shadow: 2px 2px black;
  border: 2px solid black;
  border-radius: 5px;
}

.btn i {margin-left: 5px;}

.author-info {
  width: 50%;
  margin: 25px auto;
  overflow: hidden;
  display: table;
}

.info {
  width: 100%;
  display: inline-block;
  text-align: left;
  padding-left: 20px;
}

h3 {
  color: black;
}

.author-info:hover h3 {
  color: white;
}

.info p {
  color: rgb(120, 120, 120) !important;
}

.author-info .icon {
  display: table-cell;
  vertical-align: middle;
  color: white;
}

a .author-info:hover {
  background-color: rgb(60, 60, 60);
  cursor: pointer;
}
</style>
