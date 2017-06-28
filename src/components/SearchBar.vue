<template lang="pug">
  .search-bar
    i.fa.fa-search
    input.search(
      type="search"
      placeholder="Поиск фразы"
      @input="search_phrase($event.target.value)"
      )
</template>

<script>
  export default {
    props: ['search_phrase']
  }
</script>

<style lang="stylus" scoped>
  .search-bar
    float right
    width 250px
    height 40px
    margin-top 5px
    border solid 1px #a4bdd5
    background-color #c3d6e9
    border-radius 40px
    .fa-search
      margin-left 15px
      margin-top 10px
      color #0e83be
    .search
      margin-left 10px
      background-color #c3d6e9
      border none
      // padding 0 10px
      outline none
    .search::-moz-placeholder
      color #81a1c4
    .search::-webkit-input-placeholder
      color #81a1c4
</style>
