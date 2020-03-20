<template>
  <div class="tab-control">
    <div
     v-for="(item,index) in titles"
     :key="index"
     @click="tabclick(index)"
     class="tab-control-item" 
     :class="{active: index === currentIndex}">
        <span>{{item}}</span>
     </div>
  </div>
</template>

<script>

  export default {
    name:'TabControl',
    props: {
        titles: {
            type: Array,
            default() {
                return []
            }
        }
    },
    data() {
        return {
          currentIndex: 0
        }
    },
    methods: {
        tabclick(index){  
            // console.log(this.currentIndex)         
             this.currentIndex = index;
             //传出事件,将内部的事件传给外部,index是点击了流行,新款,精选中的一个
             this.$emit('tabClick', index)
        }
    },
  }

</script>
<style scoped>
  .tab-control{
    display: flex;
    text-align: center;
    height: 40px;
    line-height: 40px;
    font-size: 15px;
  }
  .tab-control-item{
     flex: 1;
  }
  .active{
      color: line-pink;
  }
  .active span{
      padding: 5px;
      border-bottom: 3px solid pink;
  }
</style>