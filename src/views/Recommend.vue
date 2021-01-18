<template>
  <div class="recommend">
    <ScrollView>
      <div>
        <Banner :banners="banners"></Banner>
        <Personalized :personalized="personalized" :title="'推荐歌单'" @select="fatherSelectItem"></Personalized>
        <Personalized :personalized="albums" :title="'最新专辑'"></Personalized>
        <NewSong :songs="songs"></NewSong>
      </div>
    </ScrollView>
    <transition>
      <router-view></router-view>
    </transition>
  </div>
</template>

<script>
import { getBanner, getPersonalized, getNewAlbum, getNewSong } from '../api/index.js'
import Banner from '../components/Banner'
import Personalized from '../components/Personalized'
import NewSong from '../components/NewSong'
import ScrollView from '../components/ScrollView'
export default {
  name: 'Recommend',
  components: {
    Banner,
    Personalized,
    NewSong,
    ScrollView
  },
  data () {
    return {
      banners: [],
      personalized: [],
      albums: [],
      songs: []
    }
  },
  methods: {
    fatherSelectItem (id) {
      this.$router.push({
        path: `/recommend/detail/${id}`
      })
    }
  },
  created () {
    getBanner()
      .then((data) => {
        // console.log(data)
        this.banners = data.banners
      })
      .catch(function (err) {
        console.log(err)
      })
    getPersonalized()
      .then((data) => {
        // console.log(data)
        this.personalized = data.result
      })
      .catch(function (err) {
        console.log(err)
      })
    getNewAlbum()
      .then((data) => {
        // console.log(data.albums.splice(0,6))
        this.albums = data.albums.splice(0, 6)
      })
      .catch(function (err) {
        console.log(err)
      })
    getNewSong()
      .then((data) => {
        // console.log(data.albums.splice(0,6))
        this.songs = data.result
      })
      .catch(function (err) {
        console.log(err)
      })
  }
}
</script>

<style lang="scss" scoped>
  .recommend{
    position: fixed;
    top: 184px;
    left: 0;
    right: 0;
    bottom: 0;
    overflow: hidden;
  }

  .v-enter{
    transform: translateX(100%);
  }
  .v-enter-to{
    transform: translateX(0%);
  }
  .v-enter-active{
    transition: transform 1s;
  }
  .v-leave{
    transform: translateX(0%);
  }
  .v-leave-to{
    transform: translateX(100%);
  }
  .v-leave-active{
    transition: transform 1s;
  }
</style>
