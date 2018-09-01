<template>
  <div>
      <home-header></home-header>
      <home-swiper :list="swiperList"></home-swiper>
      <home-icons :list="iconList"></home-icons>
      <home-recommend :list="recommendList"></home-recommend>
      <home-weekend :list="weekendList"></home-weekend>
  </div>
</template>

<script>
import HomeHeader from './components/Header'
import HomeSwiper from './components/Swiper'
import HomeIcons from './components/Icons'
import HomeRecommend from './components/Recommend'
import HomeWeekend from './components/Weekend'
import axios from 'axios'
import {mapState} from 'vuex'
export default {
    name: 'Home',
    components: {
        HomeHeader,
        HomeSwiper,
        HomeIcons,
        HomeRecommend,
        HomeWeekend
    },
    data () {
        return {
            lastCity: '',
            swiperList: [],
            iconList: [],
            recommendList: [],
            weekendList: []
        }
    },
    methods: {
        getHomeInfo () {
            // ajax请求添加一个条件项city
            axios.get('/api/index.json?city=' + this.city)
              .then(this.getHomeInfoSucc)
        },
        getHomeInfoSucc (res) {
            res = res.data
            if (res.ret && res.data) {
                const data = res.data
                this.swiperList = data.swiperList
                this.iconList = data.iconList
                this.recommendList = data.recommendList
                this.weekendList = data.weekendList
            }
            console.log(res)
        }
    },
    computed: {
        ...mapState(['city'])
    },
    mounted () {
        this.lastCity = this.city
        this.getHomeInfo()
    },
    // 优化：当城市选择改变时，需要刷新整个页面的内容，通过lastCity这个缓存数据进行判断
    activited () {
        if (this.lastCity !== this.city) {
            this.lastCity = this.city
            this.getHomeInfo()
        }
    }
}
</script>

<style>

</style>
