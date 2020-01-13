<template>
  <div class="singer" ref="singer">
    歌手页面
  </div>
</template>

<script type="text/ecmascript-6">
  import {getSingerList} from "api/singer";
  import {ERR_OK} from "api/config";


  export default {
    data() {
      return {
        singers: []
      }
    },
    created() {
      this._getSingerList();
    },
    methods: {
      _getSingerList() {
        getSingerList().then((res) => {
          if (res.code === ERR_OK) {
            this.singers = res.data.list
          }
        })
      }
    }
  }
</script>

<style lang="stylus" scoped rel="stylesheet/stylus" type="text/stylus">
  .singer
    opsition: fixed
    top: 88px
    bottom: 0
    width: 100%
</style>
