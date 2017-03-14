<template>
  <div class="article-content">
    <div v-html="topics.content"></div>
  </div>
</template>
<style rel="stylesheet/less" lang="less">
  .article-content {
    margin: 10px auto;
    width: 100%;
  }
</style>
<script>

    export default{
        data(){
            return{

            }
        },
        props:{
          topics:{
            type:Object,
            default:()=>{
              return ''
            }
          }
        },
        components:{

        }
    }
</script>
