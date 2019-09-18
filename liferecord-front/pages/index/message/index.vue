<template>
  <div>
  <div class="imgContainer">
      <div class="bigImg">
        <div>
          <div>Message Board</div>
          <div>有什么话要跟我说的，请留言噢~~</div>
        </div>
      </div>
  </div>
  <div class="container">
    <ul>
      <li>
        <span>姓名：</span><input type="text" v-model="list.name">
      </li>
      <li>
        <span>电话：</span><input type="text" v-model="list.phone">
      </li>
      <li>
        <span>邮箱：</span><input type="text" v-model="list.email">
      </li>
      <li>
        <span>公司：</span><input type="text" v-model="list.compony">
      </li>
      <li>
        <span>留言：</span><textarea v-model="list.content"></textarea>
      </li>
      <li>
        <span>验证码：</span><input type="text" v-model="codeNum">
        <div @click="getnumCode">{{codeNum2}}</div>
      </li>
      <li>
        <span><strong>{{tips}}</strong></span>
      </li>
      <li>
        <div @click="submit">提交</div>
      </li>
    </ul>

  </div>
</div>
</template>

<script>
export default {
  data(){
    return{
      tips:'',
      list:{
        name:'',
        phone:'',
        email:'',
        compony:'',
        content:''
      },
      codeNum:'',
      codeNum2:''
    }
  },
  methods:{
    async submit(){
      let l=this.list;
      let flag=0;
      for(let i in l){
        if(l[i]==''){
          flag=1
        }
      }
      if(flag){
        this.tips='请完善信息喔~'
      }else
      if(l.name.length>20){
        this.tips='姓名长度不能超过20位喔~'
      }else
      if(!/^1[3456789]\d{9}$/.test(l.phone)){
        this.tips='手机号格式不正确喔~'
      }else
      if(!/^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/.test(l.email)){
        this.tips='邮箱格式不正确喔~'
      }else
      if(l.compony.length>30){
        this.tips='公司长度不能超过30喔~'
      }else
      if(l.content.length>200){
        this.tips='留言长度不能大于200喔~'
      }else
      if(this.codeNum2.toLowerCase()!==this.codeNum.toLowerCase()){
        this.tips='验证码不正确喔~';
      }
      else{
        this.tips='';
        const {message}=await this.$axios.$post('/api/messages',this.list);
        alert(message);
        this.list={
          name:'',
          phone:'',
          email:'',
          compony:'',
          content:''
        };
        this.codeNum='';
        this.codeNum2='';
      }
      
    },
    getnumCode(){
        let code = "";
        let codeLength = 4; //验证码的长度
        ////所有候选组成验证码的字符，当然也可以用中文的
        let codeChars = new Array(0, 1, 2, 3, 4, 5, 6, 7, 8, 9,
        'a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z',
        'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'); 
        //循环组成验证码的字符串
        for (let i = 0; i < codeLength; i++)
        {
            //获取随机验证码下标
            let charNum = Math.floor(Math.random() * 62);
            //组合成指定字符验证码
            code += codeChars[charNum];
        }
        this.codeNum2=code;
      },
  },
  mounted(){
    this.getnumCode()
  }
}
</script>

<style lang="scss" scoped>
.container{
  display: flex;
  justify-content: center;
  padding-top: 50px;
  ul{
    display: flex;
    flex-direction: column;
    align-items: center;
    li{
      margin-bottom: 40px;
      display: flex;
      align-items: center;
      span{
        color: #6c62ff;
      }
      input{
        border: 1px dashed #6c62ff;
        height: 40px;
        width: 425px;
        padding-left: 5px;
      }
      textarea{
        border: 1px dashed #6c62ff;
        height: 80px;
        width: 425px;
        padding-left: 5px;
      }
      div{
        height: 40px;
        width: 80px;
        background: #6c62ff;
        color: #fff;
        line-height: 40px;
        text-align: center;
        border-radius: 5px;
        cursor: pointer;
      }
      &:nth-child(6){
        input{
          width: 345px;
          margin-right: 5px;
        }
      }
    }
  }
}
.bigImg{
  display: flex;
  align-items: center;
  &>div{
    display:flex;
    flex-direction: column;
    align-items: center;
    margin-left: 250px;
    div{
      &:first-child{
      font-size: 60px;
      font-weight: bold;
      margin-bottom: 25px;
    }
    }
  }
}
</style>