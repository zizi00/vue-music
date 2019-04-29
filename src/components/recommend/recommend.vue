<template>
  <div class="recommend">
    <div class="recommend-content">
      <div v-if="recommends.length" class="slider-wrapper">
        <slider>
          <div v-for="(item,key) in recommends" :key="key">
            <a :href="item.linkUrl">
              <img :src="item.picUrl" />
            </a>
          </div>
        </slider>
      </div>
    </div>
  </div>
</template>
<script type="text/ecmasrcipt-6">
import {getRecommend} from '../../api/recommend.js'
import {ERR_OK} from '../../api/config.js'
import slider from '../../base/slider'
export default {
  data () {
    return {
      recommends: []
    }
  },
  created () {
    this._getRecommend()
  },
  methods: {
    _getRecommend () {
      getRecommend().then((res) => {
        if (res.code === ERR_OK) {
          this.recommends = res.data.slider
        }
      })
    }
  },
  components: {
    slider
  }
}
</script>
<style lang="stylus" scoped>

</style>
