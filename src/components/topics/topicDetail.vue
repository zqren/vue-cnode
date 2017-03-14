<template>
    <div ref="articleDetail" @scroll="displayBackTop($event)" class="article-detail">
        <!--标题信息-->
        <content-title :author="author"
                       :topics="topics"
                       :isDShow="isDShow"
                       :isCollectTopic="isCollectTopic"
                       @collect="collectTopic"
        ></content-title>
        <!--内容详情-->
        <content-detail :topics="topics"></content-detail>
        <!--回复-->
        <content-reply :replies="replies"
                       @replyUps="getUps"
        ></content-reply>
        <!--评论-->
        <content-comment :createReplyContent="createReplyContent"
                         v-model="createReplyContent"
                         @createReplies="submitReplies"></content-comment>
        <!--返回顶部-->
        <back-top :isBackTopShow="isDTopShow" @backTop="detailTop"></back-top>
        <!--加载页面-->
        <load-comp :loadShow="isDShow"></load-comp>
    </div>
</template>
<script>
  import loadComp from '../commonpage/loading'
  import backTop from '../commonpage/backTop'
  import contentTitle from './contentComp/contentTitle'
  import contentDetail from './contentComp/contentDetail'
  import contentReply from './contentComp/contentReply'
  import contentComment from './contentComp/contentComment'

  import { ACCESS_TOKEN } from '../../config'

  export default {
    data() {
      return {
        author:{},
        topics:{},
        replies:[],
        createReplyContent:'',
        isDShow:true,
        isDTopShow:false,
        isCollectTopic:false
      }
    },
    created(){
      this.getArticleDetail()
    },
    methods:{
        getArticleDetail(){
          this.$http.get(`/topic/${this.$route.params.id}`,{
            params:{
                accesstoken: ACCESS_TOKEN
            }
          })
          .then((data)=>{
             this.author = data.data.data.author
             this.topics = data.data.data
             this.replies = data.data.data.replies
             this.isCollectTopic = data.data.data.is_collect
             this.isDShow = false
          })
          .catch((error)=>{
            console.log(error)
          })
        },
       collectTopic(){
          if(this.isCollectTopic){
            this.deCollected()
          }else{
            this.collected()
          }
       },
       collected(){
            this.$http.post('/topic_collect/collect',{
              accesstoken: ACCESS_TOKEN,
              topic_id: this.$route.params.id
            })
            .then((res)=>{
                this.isCollectTopic = true
                console.group("收藏成功数据")
                console.log(res.data)
                console.groupEnd()
             })
            .catch((error)=>{
                console.group("失败数据")
                console.log(error)
                console.groupEnd()
          })
       },
       deCollected(){
           this.$http.post('/topic_collect/de_collect',{
              accesstoken: ACCESS_TOKEN,
              topic_id: this.$route.params.id
            })
            .then((res)=>{
                this.isCollectTopic = false
                console.group("取消收藏成功数据")
                console.log(res.data)
                console.groupEnd()
             })
            .catch((error)=>{
                console.group("失败数据")
                console.log(error)
                console.groupEnd()
          })
       },
       submitReplies(){
          this.$http.post(`/topic/${this.$route.params.id}/replies`,{
               accesstoken: ACCESS_TOKEN,
               content: this.createReplyContent
          })
          .then((res)=>{
              this.createReplyContent = ''
              this.getArticleDetail()
              this.$refs.articleDetail.scrollTop =  this.$refs.articleDetail.scrollHeight
          })
          .catch((error)=>{
              console.log(error)
          })
       },
       getUps(id,event){
          this.$http.post(`/reply/${id}/ups`,{
              accesstoken: ACCESS_TOKEN
          })
          .then((res) => {
             if(res.data.action == 'up'){
                event.target.classList.remove('icon-zan_light')
                event.target.classList.add('icon-zan_fill')
             }else if(res.data.action == 'down'){
                event.target.classList.remove('icon-zan_fill')
                event.target.classList.add('icon-zan_light')
             }
             this.getArticleDetail()
             console.log(res.data)
          })
          .catch((error)=>{
             console.log(error)
          })
       },
       displayBackTop(event){
          var evTop = event.target.scrollTop
          if(evTop > 100) this.isDTopShow = true
          else this.isDTopShow = false
       },
       detailTop(){
          var scrollTimer = setInterval(()=>{
              var osTop = this.$refs.articleDetail.scrollTop
              var speed = Math.floor( -osTop/6)
              this.$refs.articleDetail.scrollTop = osTop + speed
              if(osTop == 0){
                  this.isDTopShow = false
                  clearInterval(scrollTimer)
              }
          })
       }
    },
    components: {
        contentTitle,
        contentDetail,
        contentReply,
        contentComment,
        loadComp,
        backTop
    }
  }
</script>

<style lang="less" scoped>
    .article-detail {
        width: 100%;
        height: 100%;
        overflow-y: scroll;
        padding: 5px 10px;
        box-sizing: border-box;
    }
</style>
