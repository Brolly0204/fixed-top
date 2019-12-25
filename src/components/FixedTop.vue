<template>
  <div
    class="tab"
    :class="{'tab-fixed': isFixed}"
    ref="tab"
  >
    <div
      :class="{
        'tab-item': true,
        active: active === 0
      }"
      @click="selectTab(0)"
    >Tab1</div>
    <div
      :class="{
        'tab-item': true,
        active: active === 1
      }"
      @click="selectTab(1)"
    >Tab2</div>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      active: 0,
      isFixed: false,
      top: 10
    }
  },
  methods: {
    selectTab(id) {
      this.active = id
      this.handleContentScroll(id)
    },
    handleSelectTab(sTop) {
      const contents = document.querySelectorAll('.content')
      for (let i = 0; i < contents.length; i++) {
        const curContent = contents[i]
        if (sTop >= curContent.offsetTop - this.tabHeight - this.top) {
          this.active = i
        }
      }
    },
    handleContentScroll(id) {
      this.isFixed = true
      const contents = document.querySelectorAll('.content')
      const curContent = contents[id]
      this.$nextTick(() => {
        const curContentOffsetTop = curContent.offsetTop
        this.win('scrollTop', curContentOffsetTop - this.tabHeight - this.top)
      })
    },
    bindWinScroll(offsetTop) {
      window.addEventListener(
        'scroll',
        () => {
          const sTop = this.win('scrollTop')
          if (sTop >= offsetTop) {
            console.log('可以吸顶了')
            this.isFixed = true
          } else {
            this.isFixed = false
          }
          this.handleSelectTab(sTop)
        },
        false
      )
    },
    win(attr, val) {
      if (typeof val === 'undefined') {
        return document.documentElement[attr] || document.body[attr]
      }
      document.documentElement[attr] = document.body[attr] = val
    }
  },
  mounted() {
    const { tab } = this.$refs
    this.tabHeight = tab.offsetHeight
    this.bindWinScroll(tab.offsetTop)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tab {
  display: flex;
  width: 100%;
  background: #ffffff;
  box-shadow: 2px 2px 4px 1px rgba(222,222,222,1);
}

.tab-item {
  flex: 1;
  border: 1px solid #eeeeee;
  text-align: center;
}

.tab-item.active {
  color: #42b983;
  font-weight: 500;
}

.tab-fixed {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10;
}

a {
  color: #42b983;
}
</style>
