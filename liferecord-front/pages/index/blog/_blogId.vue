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
      <ul v-if="article">
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
        <span v-if="lastone" @click="lastBlog">{{lastone.blogTitle}}</span>
        <span v-else>无</span>
        <div v-if="lastone" @click="lastBlog">上一篇</div>
        <div v-else>上一篇</div>
        <div v-if="nextone" @click="nextBlog">下一篇</div>
        <div v-else>下一篇</div>
        <span v-if="nextone" @click="nextBlog">{{nextone.blogTitle}}</span>
        <span v-else>无</span>
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
            <span>朱莹辉</span>
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
          name:'全部',ifselect:true,value:5
        },
        {
          name:'前端开发',ifselect:false,value:0
        },
        {
          name:'后端开发',ifselect:false,value:1
        },
        {
          name:'生活记录',ifselect:false,value:2
        },
        {
          name:'吃喝玩乐',ifselect:false,value:3
        },
        {
          name:'环游世界',ifselect:false,value:4
        }
      ],
    }
  },
  watch:{
    $route:async function(to){
      //获取指定博客的前后共三条数据
      const data1=await this.$axios.$get('/api/blogs/checkDetail',{
        params:{
          type:to.query.type,
          page:to.query.page,
          index:to.query.index
        }
      });
      if(data1.ifFirst==true){
          this.lastone=null,
          this.article=data1.data[0],
          this.nextone=data1.data[1]
      }else{
          this.lastone=data1.data[0],
          this.article=data1.data[1],
          this.nextone=data1.data[2]
      }
    }
  },
  async asyncData(ctx){
    //获取指定博客的前后共三条数据
    const data1=await ctx.$axios.$get('/api/blogs/checkDetail',{
      params:{
        type:ctx.query.type,
        page:ctx.query.page,
        index:ctx.query.index
      }
    });
    //获取最新的五篇博客
    const data2=await ctx.$axios.$get('/api/blogs?page=1&limit=5&type=5');
    //博客各类型的数目
    const data3=await ctx.$axios.$get('/api/blogs/typeCount');
    if(data1.ifFirst==true){
      return{
        lastone:null,
        article:data1.data[0],
        nextone:data1.data[1],
        titlelist:data2.data,
        typeCount:data3.data
      }
    }else{
      return{
        lastone:data1.data[0],
        article:data1.data[1],
        nextone:data1.data[2],
        titlelist:data2.data,
        typeCount:data3.data
      }
    }
  },
  methods:{
    chooseList(index,value){
      for(let item of this.list){
        item.ifselect=false;
      }
      this.list[index].ifselect=true;
      this.$router.replace({path:'/blog',query:{
        type:value,
        page:1,
        index:0
      }})
    },
    lastBlog(){
      let objstr=JSON.stringify(this.$route.query);
      let obj=JSON.parse(objstr);
      if(obj.index*1>0){
        obj.index=obj.index-1;
      }else{
        if(obj.page*1>1){
          obj.page=obj.page-1;
          obj.index=9;
        }
      }
      this.$router.replace({path:'/blog',query:obj});
    },
    nextBlog(){
      let objstr=JSON.stringify(this.$route.query);
      let obj=JSON.parse(objstr);
      if(obj.index*1<9){
        obj.index=obj.index*1+1;
      }else{
          obj.page=obj.page*1+1;
          obj.index=0;
      }
      this.$router.replace({path:'/blog',query:obj});
    }
  },
  mounted(){
    //根据地址栏的type值确定博客类型选中的项
    for(let i=0;i<this.list.length;i++){
      if(this.list[i].value==this.$route.query.type){
        this.list[i].ifselect=true;
      }else{
        this.list[i].ifselect=false;
      }
    }
    //给博客类型添加数量
    for(let i=0;i<6;i++){
      // console.log(this.typeCount[i])
      this.$set(this.list[i],'count',this.typeCount[i]);
      // console.log(this.list)
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
          height: 120px;
          width: 120px;
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