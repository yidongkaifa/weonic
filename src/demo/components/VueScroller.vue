<template>
  <div class="page has-navbar"
       v-nav="{
      title: 'Vue Scroller',
      showBackButton: true,
      showMenuButton: true,
      menuButtonText: menuButtonText,
      onMenuButtonClick: toVueScrollerRepo
    }">
    <scroller class="page-content"
              :on-refresh="onRefresh"
              :on-infinite="onInfinite"
              ref="scroller">
      <div v-for="(item, index) in items" @click="onItemClick(index)"
           class="item item-borderless" :class="{'item-stable': index % 2 == 0}">
        {{ item }}
      </div>
    </scroller>
  </div>
</template>
<script>
  export default {
    data () {
      return {
        items: [],
        menuButtonText: '<span class="assertive">更多</span>'
      }
    },

    mounted () {
      for (let i = 1; i <= 20; i++) {
        this.items.push(i + ' - keep walking, be 2 with you.')
      }
      this.top = 1
      this.bottom = 20
      setTimeout(() => {
        if (this.$refs.scroller) {
          this.$refs.scroller.resize()
        }
      })
    },

    methods: {
      onRefresh () {
        setTimeout(() => {
          let start = this.top - 1
          for (let i = start; i > start - 10; i--) {
            this.items.splice(0, 0, i + ' - keep walking, be 2 with you.')
          }
          this.top = this.top - 10

          setTimeout(() => {
            if (this.$refs.scroller) {
              this.$refs.scroller.finishPullToRefresh()
            }
          })
        }, 1500)
      },

      onInfinite () {
        setTimeout(() => {
          let start = this.bottom + 1
          for (let i = start; i < start + 10; i++) {
            this.items.push(i + ' - keep walking, be 2 with you.')
          }
          this.bottom = this.bottom + 10

          setTimeout(() => {
            if (this.$refs.scroller) {
              this.$refs.scroller.finishInfinite()
            }
          })
        }, 1500)
      },

      onItemClick (index) {
        console.log(index)
      },

      toVueScrollerRepo () {
        window.$dialog.confirm({
          theme: 'ios',
          content: '去往 Vue Scroller 官网？'
        }).then((res) => {
          if (res) {
            location.href = 'https://wangdahoo.github.io/vue-scroller'
          }
        })
      }
    }

  }
</script>
