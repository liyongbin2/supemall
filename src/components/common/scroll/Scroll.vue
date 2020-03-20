<template>
 <div class="wrapper" ref="wrapper">
    <div class="content">
        <slot></slot>
    </div>
  </div>
</template>

<script scoped>
import BScroll from 'better-scroll'
  export default {
    name:'Scroll',
    props :{
      probeType: {
        type: Number,
        default: 0
      },
      pullUpLoda: {
        type: Boolean,
        default: false
      }
    },
    data () {
      return {
        scroll: null
      };
    },
    mounted() {
        /**
        不使用document.querySelector('.wrapper')获取wrapper，
        因为到时候界面中会有多个wrapper，不知道会取到那个组件的
        wrapper,所以应该使用ref来获取。
        ref如果是绑定在组件中，那么通过this.$refs.refname获取到的是一个组件对象。
        ref如果是绑定在普通元素中，那么通过this.$refs.refname获取到的是一个元素对象。
         */ 
        this.scroll = new BScroll(this.$refs.wrapper, {
          /**
          probeType=3代表只要有滚动都会监听
          给组件Scroll添加一个probeType动态获取probeType数值
          防止所有页面都实时监听，有些页面需要，有些页面可能不需要实时监听
           */
          probeType: this.probeType,
          //上拉加载更多用到
          pullUpLoad: this.pullUpLoda,

          /**
            默认是false，true代表div等可以进行点击监听
          */
          click: true
        })
        this.scroll.scrollTo(0,0)
          /**
            监听滚动位置,只有probeType是2或者3时才监听滚动
           */
        if (this.probeType === 2 || this.probeType === 3){
          this.scroll.on('scroll',(position) => {
          //将这个监听到的位置传出去,也就是自定义事件
          this.$emit('scroll', position)
        })
        }
        //上拉加载更多数据
        if (this.pullUpLoda) {
          this.scroll.on('pullingUp', () => { 
          /**
           * 将事件发出给home组件，因为这里是scroll组件，
           * 最终进行上拉是home组件
           * */      
          this.$emit('pullingUp')
      })  
        }

    },
    methods: {
      scrollTo(x, y, time=300) {
        this.scroll && this.scroll.scrollTo(x, y, time)
      },
      finishPullUp(){
        this.scroll && this.scroll.finishPullUp()
      },
      refresh(){
        // console.log('-------')
        this.scroll && this.scroll.refresh()
      },
      getScrollY(){
        return this.scroll ? this.$refs.saveY : 0
      }
    },
  }

</script>
<style scoped>
</style>