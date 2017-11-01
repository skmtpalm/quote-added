<template>
  <section class="section">
    <div class="container">
      <span>{{quoteCount}}/{{max}}</span>
      <progress class="progress" :class="statusClass" :value="quoteCount" :max="max"></progress>
    </div>
  </section>
</template>

<script>

export default {
  props: ['quoteCount', 'max'],
  computed: {
    statusClass() {
      if (this.quoteCount <= Math.floor(this.max / 2)) {
        return { 'is-warning': true }
      } else {
        return { 'is-danger': true }
      }
    }
  }
}

</script>

<style lang="css">
</style>
