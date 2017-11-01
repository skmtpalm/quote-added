<template>
  <div id="app">
    <app-header>
      <h1 class="title" slot="title">{{ appName }}</h1>
      <h3 class="subtitle" slot="subtitle">{{ appDescription }}</h3>
    </app-header>
    <progress-bar :max="limitQuoteCount" :quoteCount="quoteCount"></progress-bar>
    <quote-field @addQuote="addQuote" :quoteCount="quoteCount" :max="limitQuoteCount"></quote-field>
    <quotes :quotes="quotes"></quotes>
    <app-footer :author="author"></app-footer>
  </div>
</template>

<script>
import _ from 'lodash'
import { quoteBus } from './main'
import Header from './components/Header.vue'
import ProgressBar from './components/ProgressBar.vue'
import QuoteField from './components/QuoteField.vue'
import Quotes from './components/Quotes.vue'
import Footer from './components/Footer.vue'

const MAX = 10;

export default {
  components: {
    'app-header': Header,
    ProgressBar,
    QuoteField,
    Quotes,
    'app-footer': Footer
  },
  data() {
    return {
      appName: 'Quote added App',
      appDescription: 'by udemy adding Quote app limit 10',
      author: {
        name: 'Ok palm',
        url: 'http://okpalm.com'
      },
      limitQuoteCount: MAX,
      quotes: [],
      countId: 1
    }
  },
  methods: {
    addQuote(quote) {
      const newQuote = Object.assign({}, {id: this.countId}, quote)
      this.quotes.push(newQuote)
      this.countId++
    }
  },
  computed: {
    quoteCount() {
      return this.quotes.length
    }
  },
  created() {
    quoteBus.$on('deleteQuote', (id) => {
      this.quotes = this.quotes.filter(function(quote) {
        return quote.id !== id
      })
    })
    quoteBus.$on('destroyAllQuote', () => {
      this.quotes = []
    })
  }
}
</script>

<style lang="scss">
@import "../node_modules/bulma/bulma";
</style>
