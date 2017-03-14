<template>
   <div>
       <transition name="opac">
           <topic-detail v-if="$route.params.id != 'create'"></topic-detail>
           <topic-Create v-if="$route.params.id == 'create'"></topic-Create>
       </transition>
   </div>
</template>
<style rel="stylesheet/less" lang="less" scroped>
    .opac-enter-active,
    .opac-leave-active{
        transition: all .3s cubic-bezier(1.0, 0.5, 0.8, 1.0);
    }
    .opac-enter,
    .opac-leave-active{
        opacity: 0;
        transform: scale(.5);
    }
</style>
<script>
    import topicDetail from './topicDetail'
    import topicCreate from './topicCreate'

    export default{
        data(){
            return{
               
            }
        },
        components:{
            topicDetail,
            topicCreate
        }
    }
</script>
