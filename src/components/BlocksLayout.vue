<template lang="pug">
  .blocks-layout(@scroll="scroll($event)")
    .not-found(v-if="!blocks.length") По заданным условиям материалов не найдено
    video-block(
      v-for="item in blocks"
      v-if="blocks.length"
      key="item.updated_at"
      :block="item"
      )
    infinite-loading.loader(
      v-if="this.list.length < this.blocks.length"
      :on-infinite="onInfinite"
      ref="infiniteLoading"
      )
</template>

<script>
  import VideoBlock from './VideoBlock'
  import InfiniteLoading from 'vue-infinite-loading'
  export default {
    props: ['search_phrase', 'search_phrase', 'blocks', 'selected_category'],
    data () {
      return {
        list: []
      }
    },
    methods: {
      onInfinite () {
        setTimeout(() => {
          const temp = []
          for (let i = this.list.length + 1; i <= this.list.length + 20; i++) {
            if (i > this.blocks.length) return
            temp.push(this.blocks[i])
          }
          if (this.list.length >= this.blocks.length) return
          this.list = this.list.concat(temp)
          this.$refs.infiniteLoading.$emit('$InfiniteLoading:loaded')
        }, 500)
      }
    },
    computed: {
      filtredBlocks () {
        let arr = this.list.filter(block => {
          // console.log(block)
          return block.category === this.selected_category.value
        })
        return arr
      }
    },
    watch: {
      'this.blocks' () {
        console.log('watch')
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
</style>
