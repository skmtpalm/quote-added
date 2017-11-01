<template>
  <footer class="footer">
    <div class="container has-text-centered">
      <p>Code by <a :href="author.url">{{ author.name }}</a></p>
    </div>
  </footer>
</template>

<script>
export default {
  props: ['author']
}
</script>

<style lang="css">
</style>
