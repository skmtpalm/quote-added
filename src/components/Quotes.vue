<template>
  <section class="section">
    <div class="container">
      <div class="columns is-multiline">
        <div class="column is-3"
             v-for="quote in quotes"
            :key="quote.id">
          <quote-card :quote="quote"></quote-card>
        </div>
      </div>

      <notification v-if="isShowNotification" @deleteNotification="isShowNotification = false">
        <p>Info: Click on Quote to delete it</p>
      </notification>
    </div>
  </section>
</template>

<script>
import QuoteCard from './QuoteCard.vue';
import Notification from './Notification.vue'
export default {
  props: ['quotes'],
  components: {
    QuoteCard,
    Notification
  },
  data() {
    return {
      isShowNotification: false
    }
  },
  updated() {
    if (this.quotes.length > 0) {
      this.isShowNotification = true
    } else {
      this.isShowNotification = false
    }
  }
}
</script>

<style lang="css">
</style>
