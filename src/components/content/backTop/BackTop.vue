<template>
  <div
   class="back-top">
    <img src="~assets/img/upward.svg" alt="">
  </div>
</template>

<script>

  export default {
    name:'BackTop'
  }

</script>
<style scoped>
.back-top{
    position: fixed;
    right: 0px;
    bottom: 60px;
    height: 45px;
    width: 45px;
    margin-right: 15px;
    border-radius: 100%;
    background-color: white;
    
}
.back-top img{
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -25px;
    margin-left: -25px;
    width: 50px;
    height: 50px;
}
</style>