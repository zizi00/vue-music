<template>
  <div class="m-header">
    <div class="icon"></div>
    <h1 class="title">Chicken Music</h1>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="stylus" scoped>
@import '../../command/stylus/variable.styl'
@import '../../command/stylus/mixin.styl'
.m-header
  position: relative
  height: 44px
  text-align: center
  font-size: 0
  color: $color-theme
  .icon
    display: inline-block
    vertical-align: top
    margin-top: 6px
    margin-right: 9px
    width: 30px
    height: 32px
    bg-image('logo')
    background-size: 30px 32px
    background-repeat: no-repeat
  .title
    display: inline-block
    vertical-align: top
    line-height: 44px
    font-size: $font-size-large
</style>
