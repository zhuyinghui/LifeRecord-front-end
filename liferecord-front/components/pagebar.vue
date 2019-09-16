<template>
  <div class="pagebar">
      <div @click="backPage">上一页</div>
      <ul v-for="(item,index) in list" :key="index">
          <li @click="choosePage(index,item.value)" :class="{'purpleBack':item.ifselect}">{{item.value}}</li>
      </ul>
      <div @click="nextPage">下一页</div>
  </div>
</template>

<script>
export default {
  data() { 
    return {
        list:[
            {
                value:1,ifselect:true
            },
            {
                value:'...',ifselect:false
            },
            {
                value:2,ifselect:false
            },
            {
                value:3,ifselect:false
            },
            {
                value:4,ifselect:false
            },
            {
                value:'...',ifselect:false
            },
            {
                value:5,ifselect:false
            },
        ],
        currentPage:1,
    }
  },
  methods:{
      initData(){
        let maxnum=10; //最大页数
        this.list[6].value=maxnum;
      },
      choosePage(index,value){
        if(index!==1&&index!==5){
            for(let i of this.list){
                i.ifselect=false;
            }
            this.list[index].ifselect=true;
            if(index!==0&&index!==6){
                if(index==2&&this.list[index].value!==2){
                    for(let j=0;j<3;j++){
                        this.list[index+j].value=this.list[index+j].value-1;
                    }
                    this.list[index].ifselect=false;
                    this.list[index+1].ifselect=true;
                }
                if(index==3){
                    
                }
                if(index==4&&this.list[index].value!==this.list[6].value-1){
                    for(let j=0;j<3;j++){
                        this.list[index-j].value=this.list[index-j].value+1;
                    }
                    this.list[index].ifselect=false;
                    this.list[index-1].ifselect=true;
                }
            }
        this.currentPage=value;
        this.$emit('getPage',value);
        }
      },
      nextPage(){
          if(this.currentPage!==this.list[6].value){
              if(this.currentPage==this.list[6].value-1){
                  this.choosePage(6,this.list[6].value)
              }else{
                  this.choosePage(4,this.list[4].value);
              }
          }
      },
      backPage(){
          if(this.currentPage!==1){
              if(this.currentPage==2){
                  this.choosePage(0,this.list[0].value)
              }else{
                  this.choosePage(2,this.list[2].value);
              }
          }
      },
      toPageone(){
          this.choosePage(0,1);
      }
  },
  mounted(){
      this.initData()
  }
 }
</script>

<style lang="scss" scoped>
.pagebar{
    display: flex;
    margin-top: 50px;
    &>div{
        height: 40px;
        width: 100px;
        background: #6c62ff;
        color: #fff;
        font-size: 14px;
        text-align: center;
        line-height: 40px;
        border-radius: 20px 0 0 20px;
        margin-right: 5px;
        cursor: pointer;
        &:last-child{
            border-radius:0 20px 20px 0;
            margin-right: 0;
            margin-left: 5px;
        }
    }
    ul{
        li{
            height: 40px;
            width: 40px;
            border-radius: 50%;
            font-weight: bold;
            text-align: center;
            cursor: pointer;
            line-height: 40px;
            margin:0 8px;
            box-shadow: 2px 2px 12px #C4C0F9;
            &:hover{
                background: #6c62ff;
                color: #fff;
            }
        }
        .purpleBack{
            background: #6c62ff;
            color: #fff;
        }
        
    }
}
</style>