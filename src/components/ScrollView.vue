<template>
  <div id="wrapper" ref="wrapper">
    <slot></slot>
  </div>
</template>

<script>
import IScroll from 'iscroll/build/iscroll-probe'
export default {
  name: 'ScrollView',
  methods: {
    // 吧监控滚动举例的方法给外界使用
    scrolling (fn) {
      this.iscroll.on('scroll', function () {
        fn(this.y)
      })
    }
  },
  mounted () {
    this.iscroll = new IScroll(this.$refs.wrapper, {
      mouseWheel: true,
      scrollbars: false,
      probeType: 3,
      scrollX: false,
      scrollY: true,
      disablePointer: true,
      disableTouch: false,
      disableMouse: true
    })
    const observer = new MutationObserver((mutationList, observer) => {
      // console.log(mutationList)
      // console.log(this.iscroll.maxScrollY)
      this.iscroll.refresh()
      // console.log(this.iscroll.maxScrollY)
    })
    const config = {
      childList: true,
      subtree: true,
      attributeFilter: ['height', 'offsetHeight']
    }
    observer.observe(this.$refs.wrapper, config)
  }
}
</script>

<style scoped>
#wrapper{
  width: 100%;
  height: 100%;
}
</style>
