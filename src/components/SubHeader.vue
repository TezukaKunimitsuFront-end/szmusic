<template>
  <div class="header" @click="chageTheme">
    <div class="header-left" @click.stop="back"></div>
    <p class="header-title">{{title}}</p>
    <div class="header-right" @click="11"></div>
  </div>
</template>

<script>
export default {
  name: 'SubHeader',
  data () {
    return {
      themes: ['theme', 'theme1', 'theme2'],
      index: 0
    }
  },
  methods: {
    chageTheme () {
      this.index++
      if (this.index >= this.themes.length) {
        this.index = 0
      }
      document.documentElement.setAttribute('data-theme', this.themes[this.index])
    },
    back () {
      window.history.back()
    }
  },
  props: {
    title: {
      type: String,
      default: '',
      required: true
    }
  }
}
</script>

<style lang="scss">
@import"../assets/css/variable";
@import"../assets/css/mixin";

.header {
  width: 100%;
  height: 100px;
  // background: #f00;
  @include bg_color();
  display: flex;
  justify-content: space-between;
  //position: relative;
  //z-index: 999;
  .header-left,.header-right {
    width: 84px;
    height: 84px;
    margin-top: 8px;
  }
  .header-left{
    @include bg_img("../assets/images/back")
  }
  .header-right{
    @include bg_img("../assets/images/more")
  }
  .header-title {
    text-align: center;
    line-height: 100px;
    color: #fff;
    font-weight: bold;
    @include font-size($font_medium);
    @include no-wrap
  }
}
</style>
