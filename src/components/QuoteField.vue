<template>
  <div class="columns is-mobile is-centered">
    <div class="column is-half">
      <div class="field">
        <label class="label">Quote</label>
        <div class="control">
          <textarea class="textarea" placeholder="Please Write quote" ref="quote"></textarea>
        </div>
      </div>

      <div class="field">
        <label class="label">Source</label>
        <div class="control">
          <input type="text" class="input" placeholder="Person/Author etc" ref="source"></textarea>
        </div>
      </div>

      <div class="field">
        <div class="control">
          <button
            class="button is-primary"
            @click="handleAddQuote"
            :disabled="!canAdd">Add Quote</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {quoteBus} from '../main'
export default {
  props: ['quoteCount', 'max'],
  data() {
    return {
      canAdd: true
    }
  },
  methods: {
    handleAddQuote() {
      if (this.varidateAddQuote()) {
        this.canAdd = false
        this.showMessage()
        return
      }

      const quote = {
        content: this.$refs.quote.value,
        source: this.setSource(this.$refs.source.value)
      }

      this.$emit('addQuote', quote)
      this.clearFields()
    },
    setSource(source) {
      return (source !== '') ? source : 'unknown'
    },
    clearFields() {
      this.$refs.quote.value = ''
      this.$refs.source.value = ''
    },
    varidateAddQuote() {
      return this.$refs.quote.value === '' || this.quoteCount >= this.max
    },
    showMessage() {
      if (confirm('All destroy quote OK?')) {
        quoteBus.$emit('destroyAllQuote');
        this.canAdd = true
      } else {
        return
      }
    }

  }
}
</script>

<style lang="css">
</style>
