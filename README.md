# LifeRecord-front-end 
# 博客网站开发之Nuxt.js项目搭建及配置

#### 1. 进入github官网，新建仓库，克隆至本地文件夹，命令git clone https://github.com/zhuyinghui/LifeRecord-front-end.git

#### 2. 新建前端项目，命令npx create-nuxt-app liferecord-front（项目名称），新建完成后，运行项目，命令cd liferecord-front，命令npm run dev

#### 3. 进入Iconfont官网，新建图标管理项目，上传图标至项目，然后下载至本地，解压

#### 4. 将解压后的文件复制，粘贴到前端项目的static/iconfont文件夹下，打开pages/index.vue，引入iconfont，代码如下
```
import '~/static/iconfont/iconfont.css'
```
#### 5. 在static文件夹下新建common.css文件作为全局样式文件，打开nuxt.config.js，配置全局样式文件，在link数组中添加{ rel: 'stylesheet' , type:'text/css' , href:'/common.css' };
或者在assets文件夹下新建common.css文件作为全局样式文件，打开nuxt.config.js，配置全局样式文件，在css数组中加入'~assets/css/common.css'

#### 6. 新建页面，配置路由，pages/index.vue文件代码及目录结构如下
```
index.vue

<template>
  <div class="container">
    <menubar></menubar>
    <nuxt-child/>
  </div>
</template>
<script>
import menubar from '~/components/menubar.vue'
import '~/static/iconfont/iconfont.css'
export default {
  components: {
    menubar
  }
}
</script>

menubar.vue
<template>
  <div>
      <nuxt-link to="/">首页</nuxt-link>
      <nuxt-link to="blog">博客</nuxt-link>
      <nuxt-link to="message">留言板</nuxt-link>
      <nuxt-link to="author">关于作者</nuxt-link>
  </div>
</template>
```
```
pages
--index.vue
--index
----index.vue
----author
------index.vue
----blog
------index.vue
----message
------index.vue
```

#### 7. 引入sass，命令npm install --save-dev node-sass sass-loader，使用<style lang="scss" scoped></style>

#### 8. 安装字体，在网上下载字体文件思源黑体.tof和思源黑体.ttf，放置在static/font文件夹中，在common.css里面加入如下代码
```
@font-face
{
font-family: heiti;
src: url('~static/font/思源黑体.otf'),
    url('~static/font/思源黑体.ttf')
}
```

#### 9. 修改端口号，在nuxt.config.js中添加如下代码
```
server:{
    port:8080,
    host:'0.0.0.0'
}
```

### 10. 配置axios及代理解决跨域问题，安装命令npm install @nuxtjs/axios @nuxtjs/axios --save，在nuxt.config.js的配置如下，
```
  modules: [
    '@nuxtjs/axios',
    '@nuxtjs/proxy'
  ],
  axios: {
    proxy: true
  },
  proxy: {
    '/api': {
      target: 'http://localhost:3000/api/',
      pathRewrite: {
        '^/api' : '/'
      }
    }
  },
```
### 11. 异步请求数据
```
//方法一
  data(){
    return{
      count:0,
      list:[]
    }
  },
  methods:{
    async fetchSomething() {
      const data = await this.$axios.$get('/api/blogs?page=1&limit=10')
      this.list=data.data;
      this.count=data.count;
    }
  },
  mounted(){
    this.fetchSomething()
  }

//方法二，注意解构赋值的用法
  async asyncData (ctx) {
    const {count,data} = await ctx.$axios.$get('/api/blogs?page=1&limit=10')
    return { count:count, list:data }
  },

```

### 12. 路由传参，将需要参数的页面命名为“_参数名.vue”的形式，如博客详情页的目录为pages/blog/_blogId.vue，页面路由为/blog/5d7eedf4dc115a1d84de6262，在_blogId.vue里获取参数并请求数据代码如下
```
  async asyncData(ctx){
    const {data}=await ctx.$axios.$get('/api/blogs/checkDetail?blogId='+ctx.params.blogId);
    return {article:data};
  },
```
### 13. 服务端渲染应用部署，命令npm run build，npm run start