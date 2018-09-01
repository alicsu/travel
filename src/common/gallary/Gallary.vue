<template>
  <div class="container" @click="handleGallaryClick">
      <div class="wrapper">
        <swiper :options="swiperOptions">
            <swiper-slide v-for="(item, index) in imgs" :key="index">
                <img class="gallary-img" :src="item"/>
            </swiper-slide>
            <div class="swiper-pagination" slot="pagination"></div>
        </swiper>
      </div>
  </div>
</template>

<script>
export default {
    name: "CommonGallary",
    props: {
        imgs: {
            type: Array,
            default () {
                return ['http:////img1.qunarzz.com/sight/p0/1411/13/0cd5a9a57ae0d1b9b935ec604ce0f9bf.water.jpg_600x330_d6101489.jpg']
            }
        }
    },
    data () {
        return {
            swiperOptions: {
                pagination: '.swiper-pagination',
                paginationType: 'fraction',
                observeParents: true,
                observer: true,
            }
        }
    },
    methods: {
        handleGallaryClick () {
            this.$emit('close')
        },

    }
}
</script>

<style lang="stylus" scoped>
  .container >>> .swiper-container
    overflow: inherit
  .container
    display: flex
    flex-direction: column
    justify-content: center
    position: fixed
    top: 0
    right: 0
    bottom: 0
    left: 0
    z-index: 99
    background: #000
    .wrapper
      width: 100%
      .gallary-img
        width: 100%
      .swiper-pagination
        color: #ffffff
        bottom: -1rem
</style>