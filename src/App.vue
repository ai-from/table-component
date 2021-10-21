<template>
  <div id="app">
    <Table url="https://jsonplaceholder.typicode.com/posts?_limit=50" />
  </div>
</template>

<script>
import Table from '@/components/v-table'

export default {
  name: 'App',
  components: {
    Table
  }
}
</script>

<style lang="sass">
#app

</style>
