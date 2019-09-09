# LifeRecord-front-end 
# 博客网站开发（Nuxt.js+Koa+MoangoDB）

#### 1. 进入github官网，新建仓库，克隆至本地文件夹，命令git clone https://github.com/zhuyinghui/LifeRecord-front-end.git

#### 2. 新建前端项目，命令npx create-nuxt-app liferecord-front（项目名称），新建完成后，运行项目，命令cd liferecord-front，命令npm run dev

#### 3. 进入Iconfont官网，新建图标管理项目，上传图标至项目，然后下载至本地，解压

#### 4. 将解压后的文件复制，粘贴到前端项目的static/iconfont文件夹下，打开pages/index.vue，引入iconfont，代码如下
```
import '~/static/iconfont/iconfont.css'
```
#### 5. 在static文件夹下新建common.css文件作为全局样式文件，打开nuxt.config.js，配置全局样式文件在link数组中添加{ rel: 'stylesheet' , type:'text/css' , href:'/common.css' }，重启项目

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
      <nuxt-link to="home">首页</nuxt-link>
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
----author
------index.vue
----blog
------index.vue
----home
------index.vue
----message
------index.vue
```

