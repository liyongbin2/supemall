<template>
  <div class="goods-list-item">
    <img
     :src="goodsItem.show.img" alt=""
     @load="imgLoad">
    <div class="goodsinfo">
        <p>{{goodsItem.title}}</p>
        <span class="price">{{goodsItem.price}}</span>
        <span class="collect">{{goodsItem.cfav}}</span>
    </div>
  </div>
</template>

<script>

  export default {
    name:'GoodsListItem',
    props: {
        goodsItem: {
            type: Object,
            default() {
                return {}
            }
        }
    },
    data () {
      return {

      };
    },
    methods: {
        //获取图片数据是否加载
        imgLoad(){
            /**
             * $bus事件总线，通过$emit发送一个事件给$bus，
             * 在home.vue里面监听这个事件总线，如果已经得
             * 知这些图片加载完，则发送这个事件给home.vue
             * 的this.$bus.$on(),然后告诉它这个时候可以进
             * 行刷新高度了，也就是使用scroll.refresh()方
             * 法。
             * 
            */
        this.$bus.$emit('ItemImgLoad')
        }
    },

  }

</script>
<style scoped>
.goods-list-item{
    padding-bottom: 40px;
    /* margin-top: 20px */
    width: 48%;
    position: relative;
}
.goods-list-item img{
    width: 100%;
    border-radius: 0.1rem;
}
.goodsinfo{
    font-size: 12px;
    position: absolute;
    bottom: 5px;
    left: 0;
    right: 0;
    overflow: hidden;
    text-align: center;
}
.goodsinfo p{
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    margin-bottom: 3px;
}
.goodsinfo .price {
    color: red;
    margin-right: 20px;
}
.goodsinfo .collect {
    position: relative;
}
.goodsinfo .collect::before {
    content: '';
    position: absolute;
    left: -15px;
    top: -1px;
    width: 14px;
    height: 14px;
    background: url("~assets/img/星级.svg") 0 0/14px 14px
}
</style>