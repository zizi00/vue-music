<template>
  <div class="recommend">推荐页面</div>
</template>
<script type="text/ecmasrcipt-6">
import {getRecommend} from '../../api/recommend.js'
import {ERR_OK} from '../../api/config.js'
export default {
  created () {
    this._getRecommend()
  },
  methods: {
    _getRecommend () {
      getRecommend().then((res) => {
        if (res.code === ERR_OK) {
          console.log(res.data.slider)
          
        }
      })
    }
  }
}
</script>
<style lang="stylus" scoped>

</style>
