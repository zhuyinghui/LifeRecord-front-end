# LifeRecord-front-end 
# 博客网站开发（Nuxt.js+Koa+MoangoDB）

#### 1. 进入github官网，新建仓库，克隆至本地文件夹

#### 2. 新建前端项目，命令npx create-nuxt-app liferecord-front（项目名称），新建完成后，运行项目，cd liferecord-front，npm run dev

#### 3. 进入Iconfont官网，新建图标管理项目，上传图标至项目，然后下载至本地，解压

#### 4. 将解压后的文件复制，粘贴到前端项目的static/iconfont文件夹下，并在static文件夹下新建common.css文件作为全局样式文件，打开nuxt.config.js，配置全局样式文件在link数组中添加{ rel: 'stylesheet' , type:'text/css' , href:'/common.css' }，在common.css中引入iconfont代码如下，然后重启项目
```
@font-face {font-family: 'iconfont';
    src: url('iconfont.eot');
    src: url('iconfont.eot?#iefix') format('embedded-opentype'),
    url('iconfont.woff') format('woff'),
    url('iconfont.ttf') format('truetype'),
    url('iconfont.svg#iconfont') format('svg');
}
.iconfont{
    font-family:"iconfont" !important;
    font-size:16px;font-style:normal;
    -webkit-font-smoothing: antialiased;
    -webkit-text-stroke-width: 0.2px;
    -moz-osx-font-smoothing: grayscale;
}
```

