<template lang="pug">
  .sidebar-left
    .menu
      .category(
        v-for="category in categories"
        :class="{ active: category.value === active_category }"
        @click="change_category(category)"
        ) {{ category.name }}
</template>

<script>
export default {
  props: ['selected_category', 'elements_count', 'blocks', 'change_category', 'categories', 'active_category'],
  data () {
    return {
    }
  },
  methods: {
    filtered (category) {
      console.log(category)
      this.blocks = this.blocks.filter(block => {
        return block.category.indexOf(category)
      })
    }
    // changeCategory (category) {
    //   this.selected_category.name = category.name
    //   this.selected_category.value = category.value
    //   let filtred = this.blocks.filter(block => {
    //     if (this.selected_category.value === '') {
    //       return block.category
    //     } else {
    //       return block.category === this.selected_category.value
    //     }
    //   })
    //   this.elements_count.count = filtred.length
    //   this.activeCategory = category.value
    // }
  }
}
</script>

<style lang="stylus">
  .sidebar-left
    position fixed
    top 0
    margin-top 90px
    // bottom 0
    // width 250px
    // background-color #eee
    border-right solid 2px #a6c5e4
    z-index -1
    .menu
      position fixed
      width 250px
      margin-top 10px
      height 100%
      border-right solid 2px #a6c5e4
      .category
        height 50px
        color #1c3b59
        width 150px
        line-height 50px
        padding-left 20px
        float right
        clear right
        cursor pointer
        &.active
          font-weight 800
          background-color #dfebf7
</style>
