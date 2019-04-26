<template>
  <div id="app">
    <mheader></mheader>
    <tab></tab>
    <router-view></router-view>
  </div>
</template>

<script>
import mheader from './components/m-header/header'
import Tab from './components/tab/tab'
export default {
  name: 'App',
  components: {
    mheader,
    Tab
  }
}
</script>

<style>

</style>
