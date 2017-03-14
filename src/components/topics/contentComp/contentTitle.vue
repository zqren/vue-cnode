<template>
    <div class="article-title">
        <div class="header">
            <span class="author">作者 {{author.loginname}}</span>
            <span class="origin">来自：{{topics.tab | getTabName}}</span>
        </div>
        <div class="title">
            <span v-show="topics.top || topics.good">{{topics.tab | getTabName(topics.top,topics.good)}}</span>
            <span class="title">{{topics.title}}</span>
        </div>
        <div class="footer">
            <span class="dot">发布于 {{topics.create_at | getTime}}</span>
            <span class="dot">最后编辑于 {{topics.last_reply_at | getTime}}</span>
            <span class="dot">{{topics.visit_count}} 浏览</span>
            <span v-show="isDShow" class="iconfont icon-jiazai" style="font-size:10px"></span>
            <span v-show="!isDShow" @click="collectTopic">{{isCollectTopic?'已收藏':'收藏'}}</span>
        </div>
    </div>
</template>
<style rel="stylesheet/less" lang="less">
    .article-title {
        border-bottom: 1px solid #f0f0fe;
        .header {
            display: flex;
            flex-flow: row nowrap;
            align-items: center;
            justify-content: space-between;
            align-content: center;
            span {
                color: #999;
                font-size: 10px;
            }
        }
        .title {
            margin: 6px auto;
            span {
                font-size: 12px;
                display: inline-block;
                &:first-child {
                    display: inline-block;
                    width: auto;
                    height: auto;
                    padding: 2px 5px;
                    box-sizing: border-box;
                    border-radius: 3px;
                    background: #80bd01;
                    color: #fff;
                }
                &:last-child {
                    font-weight: bold;
                    color: #666;
                }
            }
        }
        .footer {
            color: #999;
            font-size: 12px;
            margin-bottom: 5px;
            span {
                margin-right: 15px;
                position: relative;
                &.dot:after {
                    position: absolute;
                    top: 6px;
                    right: -10px;
                    content: "";
                    display: block;
                    width: 4px;
                    height: 4px;
                    border-radius: 50%;
                    background: #999;
                }
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
        components:{
            
        }
    }
</script>
