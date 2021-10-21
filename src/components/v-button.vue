<template>
  <div class="v-button"
       @click="$emit('click')"
  >
    {{ title }}
  </div>
</template>

<script>
export default {
  name: 'Button',
  props: {
    title: {
      type: String,
      default: 'Кнопка'
    }
  }
}
</script>

<style lang="sass">
.v-button
  border: 1px solid black
  padding: 10px 20px
  width: min-content
  cursor: pointer
  white-space: nowrap
</style>