<template>
  <form class="article-comment" @submit.prevent="createReplies">
    <textarea :value = "value"
              @input = "updateVal($event.target.value)"
              class="comment-content"
              placeholder="输入回复内容"
    ></textarea>
    <input type="submit"
           :disabled="!value.length"
           :class="{active:value.length}"
           class="btn"
           value="提交"
    />
  </form>
</template>
<style rel="stylesheet/less" lang="less">
  .article-comment{
    position: fixed;
    bottom: 0;
    width: 100%;
    height: 32px;
    margin-left: -10px;
    display: flex;
    flex-flow: row nowrap;
    align-items: center;
    justify-content: space-between;
    textarea.comment-content{
      flex-basis: 75%;
      height: 32px;
      padding: 5px;
      box-sizing: border-box;
      border: 1px solid gainsboro;
      border-radius: 0;
      -webkit-tap-highlight-color: transparent;
      box-shadow: none;
      outline: none;
    }
    input.btn{
      height: 32px;
      flex-basis: 25%;
      border: none;
      background: rgb(83, 148, 236);
      color: #fff;
      border-radius: 0;
      -webkit-tap-highlight-color: transparent;
      &.active{
        background: #1d92ed;
        color: #fff;
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
          value:{
            type:String,
            default:''
          }
        },
        methods:{
          createReplies(){
            this.$emit('createReplies')
          },
          updateVal(val){
            this.$emit('input',val)
          },
        }
    }
</script>
