<template>
    <div class="recommend">
        <div
         class="recommend-item"
         v-for="(item,index) in recommend"
          :key="index">
            <a :href="item.link">
            <img :src="item.image"/>
            {{item.title}}
            </a>
            
        </div>
    </div>
</template>
<script>
export default {
    name: "Recommend",
    props: {
        recommend: {
            type: Array,
            default() {
                return [];
            }
        }
    }
};
</script>
<style>
  .recommend{
        display: flex;
        width: 100%;
        font-size: 12px;
        text-align: center;
        padding: 10px 0 20px;
        border-bottom: 8px solid #eee
    }
  .recommend-item{
           flex: 1;
           margin: 3px;
        }
  a{
      text-decoration:none;
      }
  .recommend-item img{
    width: 100%;
    margin-bottom: 10px;
  }
</style>