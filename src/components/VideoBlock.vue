<template lang="pug">
  .block
    .img
    .progress-bar(v-if="block.progress")
      .progress(
        v-if="block.progress"
        :id="block.updated_at"
        :style="{'width': block.progress + '%'}"
        )
    .title {{ block.title}}
    .favorited
      img(
        :src="`/static/${block.favorited ? 'heart_filled.svg' : 'heart.svg'}`"
        @click="changeFavorited(block)"
        )
    .fragments {{ block.fragments_count }} фрагмента
</template>

<script>
  export default {
    props: ['block'],
    methods: {
      changeFavorited (block) {
        this.block.favorited = !block.favorited
      }
    }
  }
</script>

<style lang="stylus">
  .block
    width 215px
    margin-top 20px
    margin-right 10px
    height 200px
    float left
    .img
      width 215px
      background-color #eee
      height 134px
      border-radius 3px
    .progress-bar
      position relative
      width 80%
      height 6px
      bottom 25px
      margin-left 10%
      background-color black
      border-radius 10px
    .progress
      position relative
      width 0
      height 6px
      background-color #00ff66
    .title
      float left
      max-width 185px
      max-height 38px
      overflow hidden
      margin-top 15px
    .favorited
      float right
      margin-top 20px
      cursor pointer
    .fragments
      float left
      clear left
      margin-top 5px
      font-size 12px
</style>
