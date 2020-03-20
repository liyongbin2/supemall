<template>
   <div id="tab-bar">
      <div
       v-for="item in tab"
       :key="item.name"
       :path="item.spath"
       @click="itemclick"
       class="tab-bar-item">
        <div>
        <img v-if="!isActive" :src="item.src" alt="">
        <img v-else :src="item.src1" alt="">
        </div>
       <div :class="{active: isActive}">{{item.txt}}</div>
       </div>
    </div>
</template>

<script>
  export default {
    name:'TabBar',
    props: {
    //   path: {
    //     type: String,
        // default: function () {
        //   return {}
        // }
        // }
      path: String
    },
    data () {
      return {
        isActive: true,
        // path: '',
        tab: [
          {
            name: 't-home',
            txt: '首页',
            spath: '/home',
            src: require('../../../assets/img/tarbar/首页.svg'),
            src1: require('../../../assets/img/tarbar/首页1.svg')
          },
          {
            name: 't-classify',
            txt: '分类',
            spath: '/category',
            src: require('../../../assets/img/tarbar/分类.svg'),
            src1: require('../../../assets/img/tarbar/分类1.svg')
          },
          {
            name: 't-shop',
            txt: '购物车',
            spath: '/cart',
            src: require('../../../assets/img/tarbar/购物.svg'),
            src1: require('../../../assets/img/tarbar/购物1.svg')
          },
          {
            name: 't-my',
            txt: '我的',
            spath: '/profile',
            src: require('../../../assets/img/tarbar/我的.svg'),
            src1: require('../../../assets/img/tarbar/我的1.svg')
          }
        ]
      };
    },
    computed: {
      // isActive() {
      //   return this.$route.Path.indexOf(this.Path) !== -1
      // }
    },
    methods: {
      itemclick() {
        // console.log(this.path)
        // console.log("555")
        this.$router.replace(this.path)
      }
    },

  }
</script>
<style>
  #tab-bar {
    display: flex;
    background: #f6f6f6;
    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;
    box-shadow: 0 -1px 1px rgba(100, 100, 100, .1);
  }
  .tab-bar-item {
    flex: 1;
    text-align: center;
    height: 49px;
    font-size: 14px;
  }
  img{
    width: 24px;
    height: 24px;
    margin-top: 3px;
  }
  .active{
    color: red;
  }
</style>