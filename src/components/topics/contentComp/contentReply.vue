<template>
  <div class="article-reply">
    <span class="reply-count">{{replies.length}}条回复</span>
    <div class="reply-content" v-for="(reply,index) in replies">
      <div class="header">
        <div class="author-avatar">
          <img :src="reply.author.avatar_url">
        </div>
        <div class="name">
          {{reply.author.loginname}}
        </div>
        <div class="floor">{{index+1}}楼</div>
        <div class="time">{{reply.create_at | getTime}}</div>
        <div class="icon">
          <span @click="replyUps(reply.id,$event)" class="iconfont icon-zan_light"></span>
          <span>{{reply.ups.length}}</span>
          <span class="iconfont icon-huifu1"></span>
        </div>
      </div>
      <div class="content" v-html="reply.content"></div>
    </div>
  </div>
</template>
<style rel="stylesheet/less" lang="less">
  .article-reply {
    border-top: 1px solid #999;
    width: 100%;
    padding-bottom: 32px;
    box-sizing: border-box;
    span.reply-count {
      display: block;
      width: 100%;
      color: #666;
      margin: 5px auto;
      font-size: 14px;
    }
    .reply-content {
      width: 100%;
      border-bottom: 1px solid gainsboro;
      div.header {
        padding: 4px 0;
        box-sizing: border-box;
        width: 100%;
        display: flex;
        flex-flow: row nowrap;
        align-items: center;
        div.author-avatar {
          flex-grow: 0;
          width: 20px;
          height: 20px;
          text-align: center;
          line-height: 20px;
          border-radius: 50%;
          background: #f1f1f0;
          img {
            width: 20px;
            height: 20px;
            border-radius: 50%;
          }
        }
        div.name{
          flex-grow: 0;
          margin-right: 10px;
          margin-left: 10px;
        }
        div.floor{
          flex-grow: 0;
          color:  #0088cc;
          position: relative;
          &:after{
            content:'';
            position: absolute;
            right:-8px;
            top:8px;
            background:  #0088cc;
            width: 5px;
            height: 5px;
            border-radius: 50%;
          }
        }
        div.time{
          flex-grow: 0;
          margin-left: 10px;
          color: #0088cc;
        }
        div.icon{
          flex-grow: 1;
          text-align: right;
          span{
            margin: 0;
            &:last-child{
              margin-left: 10px;
            }
          }
        }
      }
      .content{
        padding: 4px 0;
        box-sizing: border-box;
      }
    }
  }
</style>
<script>

    export default{
        data(){
            return{

            }
        },
        props:{
          replies:{
            type:Array,
            default:[]
          }
        },
        methods:{
          replyUps(id,event){
            this.$emit('replyUps',id,event)
          }
        }
    }
</script>
