<template>
    <div class="recommend">
      <div class="recommend-content">
        <div v-if="recommends.length" class="recommend-wrapper">
          <slider>
            <div v-for="item in recommends">
              <a :href="item.likUrl">
                <img :src="item.picUrl" alt="">
              </a>
            </div>
          </slider>
        </div>
      </div>
    </div>
</template>

<script>
  import Slider from "slider/slider"
  import {ERR_OK} from "api/config";
  import {getRecommend, getDiscList} from 'api/recommend'

  export default {
    data(){
      return {
        recommends: []
      }
    },
    created() {
      this._getRecommend();
      this._getDiscList();
    },
    methods:{
      _getRecommend(){
        getRecommend().then((res) => {
          if (res.code === ERR_OK){
            this.recommends = res.data.slider;
            // console.log(res.data.slider);
          }
        })
      },
      _getDiscList() {
        getDiscList().then((res) => {
          if (res.code === ERR_OK) {
            this.discList = res.data.list
          }
        })
      },
    },
    components: {
      Slider
    }
  }
</script>

<style lang="stylus" scoped rel="stylesheet/stylus" type="text/stylus">
  @import "~common/stylus/variable"

  .recommend
    position: fixed
    width: 100%
    top: 88px
    bottom: 0
    .recommend-content
      height: 100%
      overflow: hidden
      .slider-wrapper
        position: relative
        width: 100%
        overflow: hidden
      .recommend-list
        .list-title
          height: 65px
          line-height: 65px
          text-align: center
          font-size: $font-size-medium
          color: $color-theme
        .item
          display: flex
          box-sizing: border-box
          align-items: center /*垂直居中*/
          padding: 0 20px 20px 20px
          .icon
            /*flex-grow 一个数字，规定项目将相对于其他灵活的项目进行扩展的量。*/
            /*flex-shrink 一个数字，规定项目将相对于其他灵活的项目进行收缩的量。*/
            /*flex-basis 项目的长度。合法值："auto"、"inherit" 或一个后跟 "%"、"px"、"em" 或任何其他长度单位的数字。*/
            flex: 0 0 60px
            width: 60px
            padding-right: 20px
          .text
            display: flex
            flex-direction: column
            justify-content: center /*水平方向的对齐方式*/
            flex: 1
            line-height: 20px
            overflow: hidden
            font-size: $font-size-medium
            .name
              margin-bottom: 10px
              color: $color-text
            .desc
              color: $color-text-d
      .loading-container
        position: absolute
        width: 100%
        top: 50%
        transform: translateY(-50%)
</style>
