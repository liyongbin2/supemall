<template>
  <div class="goodslist">
  <GoodsListItem
   v-for="(item,idex) in goods"
   :key="idex"
   :goodsItem="item"/>
  </div>
</template>

<script>
import GoodsListItem from './GoodsListItem.vue'
  export default {
    name:'GoodsList',
    props: {
        goods: {
            type: Array,
            default() {
                return []
            }
        }
    },
    data () {
      return {

      };
    },
    components: {
        GoodsListItem
    }
  }

</script>
<style scoped>
.goodslist{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    padding: 2px;
}
</style>