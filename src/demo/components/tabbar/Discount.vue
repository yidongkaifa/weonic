<template>
  <div class="page has-navbar has-tabbar" v-tabbar-menu-index="1">
    <von-header theme="light">
      <span slot="title">折扣</span>
    </von-header>

    <div class="page-content padding-top">
      <p class="text-center">Discount</p>
      <item v-for="item in items" :key="item">
        discount item
      </item>
    </div>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        items: []
      }
    },

    created () {
      for (let i = 0; i < 100; i++) {
        this.items.push(i)
      }
    }
  }
</script>
