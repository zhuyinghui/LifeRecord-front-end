<template>
<div>
  <div class="imgContainer">
      <div class="bigImg">
        <div>
            <div>Welcome To My Blog</div>
            <div>我还是很喜欢你，像风走了十万八千里，不讲道理。</div>
            <div>I still like you , like the wind traveled thousands of miles , unreasonable .</div>
        </div>
      </div>
  </div>
  <div class="container">
    <ul class="menulist">
      <li v-for="(item,index) in  typelist" :key="index" @click="chooseType(item.value)" :class="{'ifselect':item.ifselect}">
        <i :class="item.icon"></i>
        <span>{{item.name}}</span>
      </li>
    </ul>
    <div class="content">
      <ul v-for="(item,n) in list" :key="n">
        <li>
          {{item.blogTitle}}
        </li>
        <li>
          <i class="iconfont iconren"></i>
          <span>{{item.userId.userName}}</span>
          <i class="iconfont iconrili1"></i>
          <span>{{item.publishTime}}</span>
        </li>
        <li>
          <div v-if="n%5==0" style="background:#6c62ff;">{{n+1}}</div>
          <div v-if="n%5==1" style="background:#fe6566;">{{n+1}}</div>
          <div v-if="n%5==2" style="background:#3fb750;">{{n+1}}</div>
          <div v-if="n%5==3" style="background:#ff7008;">{{n+1}}</div>
          <div v-if="n%5==4" style="background:#23bdb6;">{{n+1}}</div>
        </li>
        <li>
          <div v-if="n%5==0" style="color:#6c62ff;" @click="checkDetail(n)">查看详情>></div>
          <div v-if="n%5==1" style="color:#fe6566;" @click="checkDetail(n)">查看详情>></div>
          <div v-if="n%5==2" style="color:#3fb750;" @click="checkDetail(n)">查看详情>></div>
          <div v-if="n%5==3" style="color:#ff7008;" @click="checkDetail(n)">查看详情>></div>
          <div v-if="n%5==4" style="color:#23bdb6;" @click="checkDetail(n)">查看详情>></div>
        </li>
      </ul>
    </div>
    <pagebar @getPage='getPage' ref="pageBar"></pagebar>
  </div>
</div>
  
</template>

<script>
import pagebar from '@/components/pagebar'
export default {
  data(){
    return{
      typelist:[
        {
          name:'前端开发',value:0,icon:'iconfont icon_qianduankaifa',ifselect:false
        },
        {
          name:'后端开发',value:1,icon:'iconfont icon_houduankaifa',ifselect:false
        },
        {
          name:'生活记录',value:2,icon:'iconfont iconshenghuo',ifselect:false
        },
        {
          name:'吃喝玩乐',value:3,icon:'iconfont iconyoulechang',ifselect:false
        },
        {
          name:'环游世界',value:4,icon:'iconfont iconshijieditudiqiu',ifselect:false
        },
      ],
      type:5,  //当前博客类型，5代表全部博客
      page:1, //当前页码
    }
  },
  components:{
    pagebar
  },
  methods:{
    async chooseType(value){
      //保存当前博客类型
      this.type=value;
      //当前博客类型选中样式
      for(let item of this.typelist){
        item.ifselect=false;
      }
      this.typelist[value].ifselect=true;
      //获取选中类型的博客
      const {data} = await this.$axios.$get('/api/blogs?page=1&limit=10&type='+value);
      this.list=data;
      //将分页组件页码返回成1
      this.$refs.pageBar.toPageone();
    },
    async getPage(page){
      this.page=page;
      const {data} = await this.$axios.$get('/api/blogs?page='+page+'&limit=10&type='+this.type);
      this.list=data;
    },
    checkDetail(index){
      this.$router.push({path:'/blog',query:{
        type:this.type,
        page:this.page,
        index:index
      }});
      
    }
  },
  async asyncData (ctx) {
    const {data} = await ctx.$axios.$get('/api/blogs?page=1&limit=10&type=5')
    return { list:data }
  },
}
</script>

<style lang="scss" scoped>
.container{
  display: flex;
  flex-direction: column;
  align-items: center;
}
.content{
  width: 100%;
  ul{
    box-shadow: 2px 2px 17px #C4C0F9;
    margin-top: 50px; 
    padding:30px 80px 1px 30px;
    position: relative;
    &:hover{
      -webkit-transform: scale(1.03,1.03);
      transform: scale(1.03,1.03);
      -webkit-transition:-webkit-transform 0.2s;
      transition: transform 0.2s;
    }
    li{
      margin-bottom: 30px;
      &:first-child{
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
      &:nth-child(3){
        height: 60px;
        width: 60px;
        color: #fff;
        font-size: 25px;
        font-weight: bold;
        text-align: center;
        line-height: 60px;
        position:absolute;
        right: 0;
        top: 0;
        div{
          background: #6c62ff;
          border-radius: 60px 0 60px 60px;
        }
      }
      &:nth-child(4){
        font-size: 14px;
        position: absolute;
        bottom: 0;
        right: 80px;
        font-weight: bold;
        cursor: pointer;
      }
    }
  }
}
.bigImg{
  display: flex;
  align-items: center;
  &>div{
    height: 200px;
    width: 600px;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    justify-content: space-between;
    div:first-child{
      font-size: 60px;
      font-weight: bold;
      margin-bottom: 45px;
    }
  }
}
.menulist{
  width: 100%;
  height: 120px;
  display: flex;
  justify-content: space-around;
  align-items: center;
  box-shadow: 2px 2px 17px #C4C0F9;
  margin-top:-60px;
  border-radius: 5px;
  background: #fff;
  li{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: #6c62ff;
    width: 100%;
    height: 100%;
    border-radius: 5px;
    cursor: pointer;
    &:hover{
      border-bottom: 5px solid #6c62ff;
    }
    
    i{
      font-size: 58px;
      margin-bottom: 10px;
    }
  }
  .ifselect{
      border-bottom: 5px solid #6c62ff;
  }
}
</style>