<template lang="pug">
  #app
    Navbar
    SidebarLeft(
      :selected_category="selected_category"
      :elements_count="elements_count"
      :blocks="blocks"
      :change_category="changeCategory"
      :categories="categories"
      :active_category="active_category"
      )
    MainContent(
      :elements_count="elements_count"
      :selected_category="selected_category"
      :blocks="filtered"
      :search_phrase="searchPhrase"
      )
</template>
<script>
  import axios from 'axios'
  import Navbar from './components/Navbar'
  import SidebarLeft from './components/SidebarLeft'
  import MainContent from './components/MainContent'
  export default {
    name: 'app',
    data () {
      return {
        elements_count: {
          count: null
        },
        filtered: [],
        selected_category: {
          name: '',
          value: ''
        },
        phrase: {
          text: ''
        },
        blocks: [],
        active_category: '',
        categories: [
          {
            name: 'Все',
            value: '',
            active: true
          },
          {
            name: 'Ситуации',
            value: 'Situation',
            active: false
          },
          {
            name: 'Сериалы',
            value: 'Serials',
            active: false
          },
          {
            name: 'Фильмы',
            value: 'Movie',
            active: false
          },
          {
            name: 'Актеры',
            value: 'Actor',
            active: false
          },
          {
            name: 'YouTube',
            value: 'Youtube',
            active: false
          },
          {
            name: 'ТВ-шоу',
            value: 'Show',
            active: false
          },
          {
            name: 'Клипы',
            value: 'Clips',
            active: false
          }
        ]
      }
    },
    components: {
      Navbar,
      SidebarLeft,
      MainContent
    },
    methods: {
      changeCategory (category) {
        this.selected_category.name = category.name
        this.selected_category.value = category.value
        let filtred = this.blocks.filter(block => {
          if (this.selected_category.value === '') {
            return block.category
          } else {
            return block.category === this.selected_category.value
          }
        })
        this.elements_count.count = filtred.length
        this.active_category = category.value
        this.filtered = this.blocks.filter(block => {
          return block.category.includes(category.value)
        })
      },
      searchPhrase (text) {
        this.phrase = text
        this.filtered = this.blocks.filter(block => {
          return block.title.includes(text)
        })
      }
    },
    created () {
      axios.get('/static/data.json')
      .then(response => {
        this.blocks = response.data
        this.filtered = this.blocks
        this.elements_count.count = this.blocks.length
      })
      .catch(e => {
        this.errors.push(e)
      })
    }
  }
</script>
<style lang="stylus">
  body
    background-color #f5fbff
    margin 0
</style>
