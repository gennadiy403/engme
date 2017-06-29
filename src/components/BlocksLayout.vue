<template lang="pug">
  .blocks-layout
    .not-found(v-if="!blocks.length") По заданным условиям материалов не найдено
    video-block(
      v-for="item in blocks"
      v-show="blocks.length && item.title.includes(phrase)"
      key="item.title"
      :block="item"
      )
    .placeholder(v-for="item in blocks")
</template>

<script>
  import VideoBlock from './VideoBlock'
  import InfiniteLoading from 'vue-infinite-loading'
  export default {
    props: ['blocks', 'selected_category', 'phrase'],
    data () {
      return {
        list: []
      }
    },
    components: {
      VideoBlock,
      InfiniteLoading
    }
  }
</script>

<style lang="stylus">
  .blocks-layout
    margin-right -10px
    display flex
    justify-content space-between
    flex-wrap wrap
    width 100%
    top 25px
    .loader
      position relative
      width 100%
      float left
      clear left
    .not-found
      margin-top 30px
      width 100%
      color #a4bdd5
      text-align center
    .placeholder
      visibility hidden
      height 0
      width 225px
      padding 0
      margin 0
      border-top-width 0
      border-bottom-width 0
</style>
