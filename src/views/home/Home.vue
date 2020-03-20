<template>
  <div id="home">
    <NavBar class="home-nav"><div slot="center">购物街</div></NavBar>
    <TabControl
       :titles="['流行','新款','精选']"
       @tabClick="tabClick"
       ref="tabControl1"
       class="tab-control"
       v-show="isTabFixed"></TabControl>
    <Scroll
     class="content"
     ref="scroll"
     :probeType="3"
     @scroll="contentScroll"
     :pullUpLoda="true"
     @pullingUp="loadMore">
      <Recommend :recommend="recomments"></Recommend>
      <FeatureView></FeatureView>
      <TabControl
       :titles="['流行','新款','精选']"
       @tabClick="tabClick"
       ref="tabControl2"></TabControl>
       <GoodsList :goods="showGoods"></GoodsList>
    </Scroll>
    <!-- 组件不能直接监听点击@click,如果要进行组件监听需要使用@click.native -->
    <BackTop
     @click.native="backClick"
     v-show="isShowBackTop"/>
  </div>
</template>

<script>
//主页面的子组件

import Recommend from './childComps/Recommend.vue'
import FeatureView from './childComps/FeatureView.vue'

//公共组件
import NavBar from 'components/common/navbar/NavBar.vue'
import TabControl from 'components/content/tabControl/TabControl.vue'
import GoodsList from 'components/content/goods/GoodsList.vue'
import Scroll from 'components/common/scroll/Scroll.vue'
import BackTop from 'components/content/backTop/BackTop.vue'
//网络请求的js模块
import { getHomeMultidata, getHomeGoods } from "../../network/home.js"

//方法
import {debounce} from '../../commonjs/utils.js'

  export default {
    name:'Home',
    data () {
      return {
        result: [],
        recomments: [],
        goods: {
          'pop': {page: 0,list: []},
          'new': {page: 0,list: []},
          'sell': {page: 0,list: []}
        },
        currentType: 'pop',
        isShowBackTop: false,
        tabOffsetTop: 0,
        isTabFixed: false,
        saveY: 0
      };
    },
    components: {
      NavBar,
      Recommend,
      FeatureView,
      TabControl,
      GoodsList,
      Scroll,
      BackTop
    },
    computed: {
      showGoods(){
        return this.goods[this.currentType].list
      }
    },
   
    methods: {
      /**
      事件监听相关
       */
       //这个index是TabControl.vue里面tabclick(index)里
      // this.$emit('tabClick', index)传出的index
      tabClick(index) {
        // console.log(index)
        switch(index) {
          case 0:
          this.currentType = 'pop'
          break
          case 1:
          this.currentType = 'new'
          break
          case 2:
          this.currentType = 'sell'
          break
        }
        this.$refs.tabControl1.currentIndex = index;
        this.$refs.tabControl2.currentIndex = index;
      },
      //返回顶部
      backClick(){
        /**
         * 这个方法除了可以拿到属性对象外，方法也可以拿到
         * 先拿到scroll的对象，然后再调用scroll对象里面的scroll
         * 才能调用BScroll里面的scrollTo方法
         * this.$refs.scroll.scroll.scrollTo(0,0)
         * 下面是修改后的，在Scroll.vue封装一个方法
        */
        this.$refs.scroll.scrollTo(0,0)
      },
      contentScroll(position){
        //1.返回顶部按钮隐藏或出现
        // if(position.y < -1000) {
        //   this.isShowBackTop = true
        // } 
        this.isShowBackTop = position.y < -1000
        //2.tabControl吸顶
        this.isTabFixed = (-position.y) > this.tabOffsetTop
        
      },
      //上拉加载更多数据
      loadMore() {
        this.getHomeGoods(this.currentType)
      },
      /**
      网络请求相关
       */
      getHomeMultidata() {
        getHomeMultidata().then(res => {
        // console.log(res)
        //将请求的数据保存到result
        //轮播图数据
        this.result = res.data.banner.list;
        //轮播图数据下面的推荐数据
        this.recomments = res.data.recommend.list;
      })
      },
      //动态获取数据对象
      getHomeGoods(type) {
        //动态获取展示数据页数
        const page = this.goods[type].page + 1;
         getHomeGoods(type,page).then(res => {
          // console.log(res);
          this.goods[type].list.push(...res.data.list);
          this.goods[type].page++;
          //scroll默认加载一次，所以需要用finishPullUp()来完成一次加载
          this.$refs.scroll.finishPullUp()
        })
      }
    },
    created() {
      //1.请求多个数据
      this.getHomeMultidata()
      //2.请求商品数据
      this.getHomeGoods('pop')
      this.getHomeGoods('new')
      this.getHomeGoods('sell')

    },
    mounted() {
      //3.监听图片加载完成
      /**
       * 注意$bus这个东西是没有的，所以需要在原型中添加，
       * 也就是在main.js创建，也就是Vue.prototype.$bus = new Vue()，
       * 因为vue实例可以作为事件总线，所以相当于$bus是一个vue实例，所
       * 以可以通过vue实例发射和监听实例。
      */
     const refresh = debounce(this.$refs.scroll.refresh)
     debounce(this.$refs.scroll.refresh, 50)
      this.$bus.$on('ItemImgLoad',() => {
        refresh()
      })
      //获取TabControl组件里面元素的offsetTop属性
      //所有的组件都有一个属性$el：用于获取组件中的元素
      // console.log(this.$refs.tabControl.$el.offsetTop)
      this.tabOffsetTop = this.$refs.tabControl2.$el.offsetTop
    },
    destroyed() {
      console.log("-------")
    },
    activated() {
      console.log("*******")
      this.$refs.scroll.scrollTo(0,this.saveY,0)
      this.$refs.scroll.refresh()
    },
    deactivated() {
      this.saveY = this.$refs.scroll.getScrollY()
      console.log(this.$refs.scroll.getScrollY())
    },
  }

</script>
<style scoped>
#home{
  padding-top: 40px;
  height: 100vh;
  position: relative;
}
.home-nav {
  background-color: #FF1493;
  color: #ffffff;


  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 9;
}

.content{
  /* height: calc(100% - 93px);
  overflow: hidden;
  margin-top: 44px; */
  overflow: hidden;
  position: absolute;
  top: 44px;
  bottom: 49px;
}
.tab-control{
  background-color: #ffffff;
  position: relative;
  z-index: 9;
}
</style>