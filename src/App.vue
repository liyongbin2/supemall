<template>
  <div id="app">
    <keep-alive>
    <MainTabBar></MainTabBar>
    </keep-alive>
    
  </div>
  
</template>
<script>
  import MainTabBar from 'components/content/mainTabbar/MainTabBar.vue'
  export default {
    name: 'App',
    components: {
      MainTabBar
    },
  }
</script>
<style>
  @import "assets/css/base.css";

</style>
