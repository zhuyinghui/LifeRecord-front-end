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
      <li>
        <i class="iconfont icon_qianduankaifa"></i>
        <span>前端开发</span>
      </li>
      <li>
        <i class="iconfont icon_houduankaifa"></i>
        <span>后端开发</span>
      </li>
      <li>
        <i class="iconfont iconshenghuo"></i>
        <span>生活记录</span>
      </li>
      <li>
        <i class="iconfont iconyoulechang"></i>
        <span>吃喝玩乐</span>
      </li>
      <li>
        <i class="iconfont iconshijieditudiqiu"></i>
        <span>环游世界</span>
      </li>
    </ul>
    <div class="content">
      <ul v-for="n in 10" :key="n">
        <li>
          这是一篇博客的大标题这是一篇博客的大标题这是一篇博客的大标题这是一篇博客的大标题这是一篇博客的大标题这是一篇博客的大标题
        </li>
        <li>
          <i class="iconfont iconren"></i>
          <span>zhuyinghui</span>
          <i class="iconfont iconrili1"></i>
          <span>2019/9/6 上午10:35:26</span>
        </li>
        <li>
          <div v-if="n%5==1" style="background:#6c62ff;">{{n}}</div>
          <div v-if="n%5==2" style="background:#fe6566;">{{n}}</div>
          <div v-if="n%5==3" style="background:#3fb750;">{{n}}</div>
          <div v-if="n%5==4" style="background:#ff7008;">{{n}}</div>
          <div v-if="n%5==0" style="background:#23bdb6;">{{n}}</div>
        </li>
        <li>
          <div v-if="n%5==1"><a style="color:#6c62ff;" href="javasrcipt:void(0)">查看详情>></a></div>
          <div v-if="n%5==2"><a style="color:#fe6566;" href="javasrcipt:void(0)">查看详情>></a></div>
          <div v-if="n%5==3"><a style="color:#3fb750;" href="javasrcipt:void(0)">查看详情>></a></div>
          <div v-if="n%5==4"><a style="color:#ff7008;" href="javasrcipt:void(0)">查看详情>></a></div>
          <div v-if="n%5==0"><a style="color:#23bdb6;" href="javasrcipt:void(0)">查看详情>></a></div>
        </li>
      </ul>
    </div>
    <pagebar></pagebar>
  </div>
</div>
  
</template>

<script>
import pagebar from '@/components/pagebar'
export default {
  components:{
    pagebar
  },

//    async asyncData({ $axios }) {
//      console.log('被执行了v')
//       const ip = await $axios.$get('blogs?page=1&limit=10')
//       console.log(ip)
//       return { ip }
// },

  methods:{
    async fetchSomething() {
      console.log('zhixingle ')
      const ip = await this.$axios.$get('/api/blogs?page=1&limit=10')
      console.log(ip)
    }
  },
  mounted(){
    this.fetchSomething()
  }
}
</script>

<style lang="scss" scoped>
.container{
  display: flex;
  flex-direction: column;
  align-items: center;
}
.content{
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
}
</style>