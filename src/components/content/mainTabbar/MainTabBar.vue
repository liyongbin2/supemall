<template>
  <div>
    <router-view></router-view>
   <TabBar>
    <TabBarItem path="/home">
    <img slot="item-icon" src="../../../assets/img/tarbar/首页.svg" alt="111">
    <img slot="item-icon-active" src="../../../assets/img/tarbar/首页1.svg" alt="">
    <div slot="item-text">首页</div>
    </TabBarItem>
    <TabBarItem path="/category">
    <img slot="item-icon" src="../../../assets/img/tarbar/分类.svg" alt="">
     <img slot="item-icon-active" src="../../../assets/img/tarbar/分类1.svg" alt="">
    <div slot="item-text">分类</div>
    </TabBarItem>
    <TabBarItem path="/cart">
    <img slot="item-icon" src="../../../assets/img/tarbar/购物.svg" alt="">
     <img slot="item-icon-active" src="../../../assets/img/tarbar/购物1.svg" alt="">
    <div slot="item-text">购物</div>
    </TabBarItem>
    <TabBarItem path="/profile">
    <img slot="item-icon" src="../../../assets/img/tarbar/我的.svg" alt="">
     <img slot="item-icon-active" src="../../../assets/img/tarbar/我的1.svg" alt="">
    <div slot="item-text">我的</div>
    </TabBarItem>
   </TabBar>
  </div>
</template>

<script>
  import TabBar from 'components/common/tabbar/TabBar'
  import TabBarItem from 'components/common/tabbar/TabBarItem'
  export default {
    name:'MainTabBar',
    components: {
      TabBar,
      TabBarItem
    },
  }

</script>
<style scoped>

</style>