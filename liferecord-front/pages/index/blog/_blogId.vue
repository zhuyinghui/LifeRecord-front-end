<template>
  <div>
  <div class="imgContainer">
      <div class="bigImg">
        <div>
          <div>Blog List</div>
            <ul>
              <li v-for="(item,index) in titlelist" :key="index">{{item.blogTitle}}</li>
              <li>...</li>
            </ul>
          </div>  
        </div>
  </div>
  <div class="container">
    <div class="article">
      <ul>
        <li>{{article.blogTitle}}</li>
        <li>
          <i class="iconfont iconren"></i>
          <span>{{article.userId.userName}}</span>
          <i class="iconfont iconrili1"></i>
          <span>{{article.publishTime}}</span>
        </li>
        <li>
          <div v-html="article.blogContent"></div>
        </li>
      </ul>
      <div>
        <span>这是上一篇博客的文章标题{{type}}</span>
        <div>上一篇</div>
        <div>下一篇</div>
        <span>这是下一篇博客的文章标题这是下一篇博客的文章标题这是下一篇博客的文章标题</span>
      </div>
    </div>
    <div class="sider">
      <div>
        <span>博客分类</span>
        <ul>
          <li @click="chooseList(index,item.value)" v-for="(item,index) in list" :key="index" :class="{'purpleBack':item.ifselect}">
            <span>{{item.name}}</span><span>{{item.count}}</span>
          </li>
        </ul>
      </div>
      <div>
        <img src="~static/headImg.png" alt="">
        <ul>
          <li>
            <span>朱莹辉</span><span>前端工程师</span>
          </li>
          <li>1998.05.01</li>
          <li>湖南财政经济学院</li>
        </ul>
      </div>
      <div>
        <input type="text" placeholder="搜索博客">
        <i class="iconfont iconsousuo"></i>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  data(){
    return{
      list:[
        {
          name:'全部',count:100,ifselect:true,value:5
        },
        {
          name:'前端开发',count:20,ifselect:false,value:0
        },
        {
          name:'后端开发',count:20,ifselect:false,value:1
        },
        {
          name:'生活记录',count:20,ifselect:false,value:2
        },
        {
          name:'吃喝玩乐',count:20,ifselect:false,value:3
        },
        {
          name:'环游世界',count:20,ifselect:false,value:4
        }
      ],
    }
  },
  async asyncData(ctx){
    //获取博客详情
    const data1=await ctx.$axios.$get('/api/blogs/checkDetail',{
      params:{
        blogId:ctx.params.blogId,
        page:ctx.query.page,
        index:ctx.query.index
      }
    });
    //获取最新的五篇博客
    const data2=await ctx.$axios.$get('/api/blogs?page=1&limit=5&type=5');
    //获取当前博客的上一条和下一条记录
    
    return{
      article:data1.data,
      titlelist:data2.data,
      type:ctx.query.type
    }
  },
  methods:{
    chooseList(index,value){
      for(let item of this.list){
        item.ifselect=false;
      }
      this.list[index].ifselect=true;
      this.type=value;
      // const data=await this.$axios.$get('api/blogs/')
    }
  },
  mounted(){
    //根据地址栏的type值确定博客类型选中的项
    for(let i=0;i<this.list.length;i++){
      if(this.list[i].value==this.type){
        this.list[i].ifselect=true;
      }else{
        this.list[i].ifselect=false;
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.container{
  display: flex;
  margin-top: 50px;
  
  .sider{
    width: 30%;
    div{
      width: 100%;
      box-shadow: 1px 1px 15px rgba(108,98,255,0.15);
      &:first-child{
        display: flex;
        flex-direction: column;
        align-items: center;
        &>span{
          padding: 20px 0;
          font-size: 18px;
          font-weight: bold;
          color: #6c62ff;
        }
        ul{
          width: 100%;
          li{
            width: 100%;
            padding:10px 40px;
            display: flex;
            justify-content: space-between;
            color: #6c62ff;
            font-weight: bold;
            cursor: pointer;
            &:hover{
              background: #6c62ff;
              color:#fff;
              -webkit-transform: scale(1.03,1);
              transform: scale(1.03,1);
              -webkit-transition:-webkit-transform 0.2s;
              transition: transform 0.2s;
            }
          }
          .purpleBack{
            background: #6c62ff;
            color:#fff;
          }
        }
      }
      &:nth-child(2){
        height: 160px;
        margin-top: 30px;
        padding:20px;
        display: flex;
        align-items: center;
        justify-content: center;
        img{
          height: 100px;
          width: 100px;
          margin-right: 15px;
        }
        ul{
          li{
            width:128px;
            margin-bottom: 12px;
            &:first-child{
              display: flex;
              span{
                &:first-child{
                  font-weight: bold;
                  margin-right: 15px;
                }
                &:last-child{
                  font-size: 10px;
                  display: block;
                  background: #6c62ff;
                  color: #fff;
                  line-height: 24px;
                  padding: 0 5px;
                }
              }
              
            }
          }
        }
      }
      &:nth-child(3){
        height: 115px;
        margin: 30px 0 50px 0;
        display: flex;
        align-items: center;
        justify-content: center;
        input{
          height: 50px;
          width: 80%;
          border: 1px dashed #6c62ff;
          padding-left: 15px;
          border-radius: 25px;
        }
        i{
          color: #6c62ff;
          font-size: 25px;
          margin-left: -35px;
        }
      }
    }
  }
  .article{
    width: 67%;
    margin-right: 3%;
    box-shadow: 1px 1px 15px rgba(108,98,255,0.15);
    padding:30px;
    ul li{
      margin-bottom: 20px;
      &:first-child{
        font-size: 18px;
        font-weight: bold;
      }
      &:nth-child(2){
        font-size: 12px;
        display: flex;
        align-items: center;
        i,span{
          color: #6c62ff;
          padding-right: 10px;
          &:last-of-type{
            color: #fe6566;
          }
        }
        i{
          font-size: 25px;
        }
        span:first-of-type{
            margin-right: 25px;
        }
      }
    }
    &>div{
      display: flex;
      font-size: 12px;
      align-items: center;
      justify-content: space-between;
      margin-top: 50px;
      span{
        width: 30%;
        text-decoration: underline;
        color: #6c62ff;
        cursor: pointer;
        &:first-of-type{
          text-align: right;
        }
      }
      div{
        width: 15%;
        background: #6c62ff;
        color: #fff;
        text-align: center;
        padding:10px 0;
        cursor: pointer;
        &:first-of-type{
          border-radius: 20px 0 0 20px;
        }
        &:last-of-type{
          border-radius:0 20px 20px 0;
        }
      }
    }
  }
  

}


.bigImg{
  display: flex;
  align-items: center;
  &>div{
    width: 450px;
    margin-left: 100px;
    div{
       font-size: 60px;
      font-weight: bold;
      margin-bottom: 25px;
    }
    ul li{
        height: 24px;
        overflow: hidden;
        margin-bottom: 10px;
    }
  }
}
</style>