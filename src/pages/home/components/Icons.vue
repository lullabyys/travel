<template>
  <div class="icons">
      <swiper class="swiper-content" :options="swiperOptions">
          <swiper-slide v-for="(page,index) of pages" :key="index">
            <div class="icon" v-for="item of page" :key="item.id">
                <div class="icon-img">
                    <img class="icon-img-content" :src="item.imgUrl" alt="" />
                    </div>
                <p class="icon-desc">{{item.desc}}</p>
            </div>
          </swiper-slide>
      </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeIcons',
  props: {
    list: Array
  },
  data () {
    return {
      swiperOptions: {
        autoplay: false
        // Some Swiper option/callback...
      }
    }
  },
  computed: {
    pages: function () {
      const pages = []
      this.list.forEach((item, index) => {
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  }
}
</script>
<style lang="stylus" scoped>
@import '~styles/varibles.styl';
@import '~styles/mixins.styl';
  .icons >>> .swiper-content{
    height: 0;
    padding-bottom: 50%;
  }
  .icons{
    //   width可以省略，因为是个 div标签，占一行。
    margin-top 0.1rem
    width: 100%;
    overflow: hidden;
    height: 0;
    padding-bottom: 50%;
    .icon{
      position relative
      overflow hidden
      float: left
      height 0
      width: 25%;
      padding-bottom: 25%;
      .icon-img{
        position absolute
        top 0
        left 0
        right 0
        bottom 0.44rem
        box-sizing border-box
        padding 0.1rem
        .icon-img-content{
          height 100%
          display block
          margin 0 auto
        }
      }
      .icon-desc{
        position absolute
        left 0
        right 0
        bottom 0
        height 0.44rem
        line-height 0.44rem
        text-align center
        color $darkTextColor
        ellipsis()
      }
    }
  }
</style>
