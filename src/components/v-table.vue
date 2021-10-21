<template>
  <div class="v-table">

    <div class="v-table__head">
      <div class="v-table__head-userid" @click="sort('userId')">UserId</div>
      <div class="v-table__head-id" @click="sort('id')">Id</div>
      <div class="v-table__head-title" @click="sort('title')">Title</div>
      <div class="v-table__head-body" @click="sort('body')">Body</div>
    </div>

    <div class="v-table__item"
      v-for="(item, index) in json"
      :key="index"
    >
      <div class="v-table__item-userid">{{ item.userId }}</div>
      <div class="v-table__item-id">{{ item.id }}</div>
      <div class="v-table__item-title">{{ item.title }}</div>
      <div class="v-table__item-body">{{ item.body }}</div>
    </div>

    <Button
      title="Загрузить еще..."
      @click="upload"
    />

  </div>
</template>

<script>
import Button from '@/components/v-button'

export default {
  name: 'Table',
  components: {
    Button
  },
  data() {
    return {
      json: [],
      step: 10,
      sortingColumns: {
        'userId': true,
        'id': true,
        'title': true,
        'body': true
      },
      mainKey: ''
    }
  },
  props: {
    url: {
      type: String,
      required: true
    }
  },
  methods: {
    async getData() {
      let response = await fetch(this.url)
      if(response.ok) {
        this.json = await response.json()
        this.json = this.json.filter((item, index) => index < this.step)
      } else {
        alert('Error: ' + response.status)
      }
    },
    sort(param) {
      if(this.sortingColumns[param]) {
        this.json.sort((a, b) => (a[param] > b[param]) ? 1 : (b[param] > a[param]) ? -1 : 0)
      } else {
        this.json.sort((a, b) => (a[param] > b[param]) ? -1 : (b[param] > a[param]) ? 1 : 0)
      }
      this.sortingColumns[param] = !this.sortingColumns[param]
      this.mainKey = param
    },
    async upload() {
      this.step += 10
      await this.getData()
      if(!this.sortingColumns[this.mainKey]) {
        this.json.sort((a, b) => (a[this.mainKey] > b[this.mainKey]) ? 1 : (b[this.mainKey] > a[this.mainKey]) ? -1 : 0)
      } else {
        this.json.sort((a, b) => (a[this.mainKey] > b[this.mainKey]) ? -1 : (b[this.mainKey] > a[this.mainKey]) ? 1 : 0)
      }
    }
  },
  created() {
    this.getData()
  }
}
</script>

<style lang="sass">
.v-table
  display: grid
  grid-template-rows: repeat(2, min-content)
  grid-row-gap: 10px
  &__head
    display: grid
    grid-template-columns: repeat(4, 1fr)
    grid-column-gap: 10px
  &__item
    display: grid
    grid-template-columns: repeat(4, 1fr)
    grid-column-gap: 10px
</style>