<template>
    <div class="song">
      <div class="song-top">
        <h3>新歌推荐</h3>
      </div>
      <ul class="song-list">
        <li v-for="song in songs" :key="song.id" class="item" >
          <img v-lazy="song.picUrl" alt="">
          <div>
            <h3>{{song.name}}</h3>
            <p>{{song.song.artists[0].name}}</p>
          </div>
        </li>
      </ul>
    </div>
</template>

<script>
export default {
  name: 'NewSong',
  props: {
    songs: {
      type: Array,
      default: () => [],
      required: true
    }
  }
}
</script>

<style scoped lang="scss">
  @import "../assets/css/mixin";
  @import "../assets/css/variable";
.song{
  width: 100%;
  @include bg_sub_color;
  .song-top{
    width: 100%;
    height: 84px;
    line-height: 84px;
    @include bg_sub_color();
    padding: 0 20px;
    border-bottom: 1px solid #ccc;
    h3{
      @include font_size($font_large);
      font-weight: bold;
      @include  font_color();
    }
  }
}
.song-list{
  width: 100%;
  overflow: hidden;
  .item{
    width: 100%;
    height: 200px;
    display: flex;
    align-items: center;
    padding: 0 20px;
    margin-bottom: 20px;
    border-bottom: 1px solid #ccc;
    img{
      width: 150px;
      height: 150px;
      border-radius: 20px;
      margin-right: 20px;
    }
    div{
      h3{
        @include  font_size($font_large);
        @include font_color
      }
      p{
        @include  font_size($font_samll);
        @include font_color;
        opacity: 0.6;
        margin-top: 20px;
      }
    }
  }
}
</style>
