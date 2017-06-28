<template lang="pug">
  .order-bar
    .category {{ selected_category.name || 'Все' }}
    .elements-count {{ elements_count.count }} подборок
    .order(@click="ui.sort_dropdown = !ui.sort_dropdown") {{ ui.order.name || 'Сначала популярные' }}
      i.fa.fa-caret-down
    .order-dropdown(v-show="ui.sort_dropdown")
      .item(
        v-for="item in orders"
        @click="setOrder(item)"
        ) {{ item.name }}
</template>

<script>
export default {
  props: ['selected_category', 'blocks', 'elements_count'],
  data () {
    return {
      ui: {
        sort_dropdown: false,
        order: {
          name: ''
        }
      },
      orders: [
        {
          id: 1,
          name: 'Сначала популярные'
        },
        {
          id: 2,
          name: 'Сначала новые'
        }
      ]
    }
  },
  methods: {
    setOrder (item) {
      this.ui.order.name = item.name
      this.ui.sort_dropdown = false
      if (item.id === 1) {
        this.sortByPopularity(this.blocks, this.ui.order.name)
      } else if (item.id === 2) {
        this.sortByDate(this.blocks, this.ui.order.name)
      }
    },
    sortByPopularity (items) {
      items.sort(function (a, b) {
        console.log(a.popularity)
        if (a.popularity > b.popularity) {
          return -1
        }
        if (a.popularity < b.popularity) {
          return 1
        }
        return 0
      })
      console.log(items)
    },
    sortByDate (items) {
      items.sort(function (a, b) {
        console.log(a.updated_at)
        if (a.updated_at > b.updated_at) {
          return -1
        }
        if (a.updated_at < b.updated_at) {
          return 1
        }
        return 0
      })
      console.log(items)
    }
  }
}
</script>

<style lang="stylus">
  .order-bar
    float left
    width 300px
    .category
      position relative
      float left
      font-size 22px
    .elements-count
      position relative
      float left
      font-size 14px
      margin-left 10px
      margin-top 8px
      color #0e83be
      cursor pointer
    .order
      float left
      clear left
      margin-top 5px
      color #0e83be
      cursor pointer
      i
        margin-left 5px
    .order-dropdown
      position absolute
      top 50px
      width 200px
      .item
        height 30px
        border-bottom solid 1px #c5c5c5
        border-right solid 1px #c5c5c5
        border-left solid 1px #c5c5c5
        float left
        cursor pointer
        line-height 30px
        padding 0 10px
        width 100%
        background-color #fff
        &:first-child
          border-top solid 1px #c5c5c5
        &:hover
          background-color #dfebf7

</style>
