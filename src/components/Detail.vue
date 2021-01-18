<template>
<div class="detail">
<SubHeader :title="list.name"></SubHeader>
  <DetailTop :face="list.coverImgUrl" ref="top"></DetailTop>
  <div class="bottom">
  <ScrollView ref="scrollview">
      <DetailBottom :playlist="list.tracks"></DetailBottom>
  </ScrollView>
  </div>
</div>
</template>

<script>
import SubHeader from '../components/SubHeader'
import DetailTop from '../components/DetailTop'
import DetailBottom from '../components/DetailBottom'
import ScrollView from '../components/ScrollView'

import { getPlayList } from '../api/index'
export default {
  name: 'Detail',
  data: function () {
    return {
      list: []
    }
  },
  components: {
    SubHeader,
    DetailTop,
    DetailBottom,
    ScrollView
  },
  created () {
    getPlayList({ id: this.$route.params.id })
      .then((data) => {
        // console.log(data)
        this.list = data.playlist
      })
      .catch(function (err) {
        console.log(err)
      })
  },
  mounted () {
    const defaultHeight = this.$refs.top.$el.offsetHeight

    this.$refs.scrollview.scrolling((offsetY) => {
      if (offsetY < 0) {
        const scale = 20 * Math.abs(offsetY) / defaultHeight
        this.$refs.top.$el.style.filter = `blur(${scale}px)`
      } else {
        const scale = 1 + offsetY / defaultHeight
        this.$refs.top.$el.style.transform = `scale(${scale})`
        console.log(scale)
      }
    })
  }
}
</script>

<style scoped lang="scss">
  @import "../assets/css/mixin";
.detail{
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  @include bg_sub_color
  }

.bottom {
  position: fixed;
  top: 500px;
  bottom: 0;
  left: 0;
  right: 0;
}
</style>
