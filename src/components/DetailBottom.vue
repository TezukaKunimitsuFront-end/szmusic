<template>
    <ul class="detail-bottom">
      <li class="bottom-top">
        <div class="bottom-icon"></div>
        <div class="bottom-title">播放全部</div>
      </li>
      <li v-for="song in playlist" :key="song.id" class="item">
        <h3>{{song.name}}</h3>
        <p>{{song.al.name}} - {{song.ar[0].name}}</p>
      </li>
    </ul>
</template>

<script>
export default {
  name: 'DetailBottom',
  props: {
    playlist: {
      type: Array,
      default: () => [],
      required: true
    }
  }
}
</script>

<style scoped lang="scss">
  @import "../assets/css/variable";
  @import "../assets/css/mixin";
.detail-bottom{
  width: 100%;
  li{
    width: 100%;
    height: 100px;
    padding: 20px;
    box-sizing: border-box;
    @include  bg_sub_color;
    border-top: 1px solid #ccc;
  }
  .bottom-top{
    display: flex;
    align-items: center;
    border-top-left-radius:50px;
    border-top-right-radius: 50px;
    .bottom-icon{
      width: 60px;
      height: 60px;
      @include  bg_img('../assets/images/small_play');
      margin-right: 20px;
    }
    .bottom-title{
      @include font_size($font_large);
      @include  font_color
    }
  }
  .item{
    h3{
      @include font_color;
      @include font_size($font_medium);
    }
    p{
      @include font_color;
      @include font_size($font_samll);
      margin-top: 10px;
      opacity: 0.8;
    }
  }
}
</style>
