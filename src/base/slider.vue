<template>
  <div class="slider" ref="slider">
    <div class="slider-group" ref="slidergroup">
      <slot></slot>
    </div>
    <div class="dots">
      <span class="dot" v-for="(item,index,key) in dots" :key="key" :class="{active: currentIndex===index}"></span>
    </div>
  </div>
</template>
<script type="text/ecmasrcipt-6">
import BScroll from 'better-scroll'
import { setTimeout, clearTimeout } from 'timers'
import {addClass} from '../command/js/dom.js'
export default {
  data () {
    return {
      dots: [],
      currentIndex: 0
    }
  },
  props: {
    loop: {
      type: Boolean,
      default: true
    },
    autoPlay: {
      type: Boolean,
      default: true
    },
    interval: {
      type: Number,
      default: 4000
    }
  },
  mounted () {
    setTimeout(() => {
      this._setsliderwidth()
      this._initdots()
      this._initslider()
      if (this.autoPlay) {
        this._play()
      }
    }, 20)
    window.addEventListener('resize', () => {
      if (!this.slider) {
        return
      }
      this._setsliderwidth(true)
      this.slider.refresh()
    })
  },
  methods: {
    _setsliderwidth (isresize) {
      this.children = this.$refs.slidergroup.children
      let width = 0
      let sliderwidth = this.$refs.slider.clientWidth
      for (let i = 0; i < this.children.length; i++) {
        let child = this.children[i]
        addClass(child, 'slider-item')
        child.style.width = sliderwidth + 'px'
        width += sliderwidth
      }
      if (this.loop && !isresize) {
        width += (2 * sliderwidth)
      }
      this.$refs.slidergroup.style.width = width + 'px'
    },
    _initdots () {
      this.dots = new Array(this.children.length)
    },
    _initslider () {
      this.slider = new BScroll(this.$refs.slider, {
        scrollX: true,
        scrollY: false,
        momentum: false,
        snap: {
          loop: this.loop,
          threshold: 0.3,
          speed: 400
        },
        click: true
      })
      this.slider.on('scrollEnd', () => {
        let pageIndex = this.slider.getCurrentPage().pageX
        this.currentIndex = pageIndex
        if (this.autoPlay) {
          clearTimeout(this.timer)
          this._play()
        }
      })
    },
    _play () {
      let pageIndex = this.currentIndex + 1
      if (pageIndex === this.dots.length) {
        pageIndex = 0
      }
      this.timer = setTimeout(() => {
        this.slider.goToPage(pageIndex, 0, 400)
      }, this.interval)
    }
  },
  destroyed () {
    clearTimeout(this.timer)
  }
}
</script>
<style lang="stylus" scoped>
@import '../command/stylus/variable.styl'
.slider
  position: relative
  min-height: 1px
  .slider-group
    position: relative
    overflow: hidden
    white-space: nowrap
    .slider-item
      float: left
      box-sizing: border-box
      overflow: hidden
      text-align: center
      a
        display: block
        width: 100%
        overflow: hidden
        img
          display: block
          width: 100%
  .dots
    position: absolute
    right: 0
    left: 0
    bottom: 12px
    text-align: center
    font-size: 0
    .dot
      display: inline-block
      margin-right: 4px
      width: 8px
      height: 8px
      border-radius: 50%
      background: $color-text-l
      &.active
        width: 20px
        border-radius: 5px
        background: $color-text-ll
</style>
