<template>
  <div class="notification is-info">
    <button
      class="delete"
      @click="handleDeleteThis"
      ></button>
    <slot></slot>
  </div>
</template>

<script>
export default {
  methods: {
    handleDeleteThis() {
      this.$emit('deleteNotification')
    }
  }
}
</script>

<style lang="css">
</style>
