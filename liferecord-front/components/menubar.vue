<template>
  <div class="menubar" :class="{'backcolor':ifbackcolor}">
    <ul class="menu">
      <li>
        LifeRecord
      </li>
      <li>
        <nuxt-link to="/">首页</nuxt-link>
      </li>
      <li>
        <nuxt-link :to="'/blog/'+'?type=5&page=1&index=0'">博客</nuxt-link>
      </li>
      <li>
        <nuxt-link to="/message">留言板</nuxt-link>
      </li>
      <li>
        <nuxt-link to="/author">关于作者</nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data(){
    return{
      ifbackcolor:false,
    }
  },
  mounted(){
    window.onscroll=()=>{
      let t = document.documentElement.scrollTop||document.body.scrollTop;
      if(t>90){
        this.ifbackcolor=true;
      }else{
        this.ifbackcolor=false;
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  .menubar{
    width:100%;
    height: 90px;
    position: fixed;
    top:0;
    z-index: 2;
  }
  .menu{
    height: 100%;
    width: 80%;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    min-width: 350px;
  }
  .menu li{
    width: 10%;
    min-width: 64px;
    text-align: center;
    height: 100%;
    line-height: 90px;
    &:nth-child(2):hover,
    &:nth-child(3):hover,
    &:nth-child(4):hover,
    &:nth-child(5):hover{
      background: #5E55FB;
    }
  }
  .menu li:first-child{
    color: #fff;
    width: 60%;
    text-align: left;
    font-size: 25px;
    font-weight: bold;
  }
  .menu li a{
    color: #fff;
  }
  .backcolor{
    background: #6c62ff;
    box-shadow: 2px 2px 15px rgba(0, 0, 0, 0.2)
  }
</style>
