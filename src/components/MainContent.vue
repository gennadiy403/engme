<template lang="pug">
  .content
    order-bar(
      :selected_category="selected_category"
      :blocks="blocks"
      :elements_count="elements_count"
      )
    search-bar(
        :search_phrase="search_phrase"
      )
    blocks-layout(
      :selected_category="selected_category"
      :blocks="blocks"
      :phrase="phrase"
      )
</template>

<script>
  import OrderBar from './OrderBar'
  import SearchBar from './SearchBar'
  import BlocksLayout from './BlocksLayout'
  export default {
    props: ['selected_category', 'blocks', 'elements_count', 'search_phrase', 'phrase'],
    components: {
      OrderBar,
      SearchBar,
      BlocksLayout
    },
    watch: {
      'selected_category' () {
        console.log(123)
      }
    }
  }
</script>

<style lang="stylus">
  .content
    position absolute
    left 250px
    right 70px
    margin-top 15px
    margin-left 30px
</style>
