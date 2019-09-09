# LifeRecord-front-end 
# ������վ������Nuxt.js+Koa+MoangoDB��

#### 1. ����github�������½��ֿ⣬��¡�������ļ��У�����git clone https://github.com/zhuyinghui/LifeRecord-front-end.git

#### 2. �½�ǰ����Ŀ������npx create-nuxt-app liferecord-front����Ŀ���ƣ����½���ɺ�������Ŀ������cd liferecord-front������npm run dev

#### 3. ����Iconfont�������½�ͼ�������Ŀ���ϴ�ͼ������Ŀ��Ȼ�����������أ���ѹ

#### 4. ����ѹ����ļ����ƣ�ճ����ǰ����Ŀ��static/iconfont�ļ����£���pages/index.vue������iconfont����������
```
import '~/static/iconfont/iconfont.css'
```
#### 5. ��static�ļ������½�common.css�ļ���Ϊȫ����ʽ�ļ�����nuxt.config.js������ȫ����ʽ�ļ���link���������{ rel: 'stylesheet' , type:'text/css' , href:'/common.css' }��������Ŀ

#### 6. �½�ҳ�棬����·�ɣ�pages/index.vue�ļ����뼰Ŀ¼�ṹ����
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
      <nuxt-link to="home">��ҳ</nuxt-link>
      <nuxt-link to="blog">����</nuxt-link>
      <nuxt-link to="message">���԰�</nuxt-link>
      <nuxt-link to="author">��������</nuxt-link>
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

