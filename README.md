# LifeRecord-front-end 
# ������վ����֮Nuxt.js��Ŀ�������

#### 1. ����github�������½��ֿ⣬��¡�������ļ��У�����git clone https://github.com/zhuyinghui/LifeRecord-front-end.git

#### 2. �½�ǰ����Ŀ������npx create-nuxt-app liferecord-front����Ŀ���ƣ����½���ɺ�������Ŀ������cd liferecord-front������npm run dev

#### 3. ����Iconfont�������½�ͼ�������Ŀ���ϴ�ͼ������Ŀ��Ȼ�����������أ���ѹ

#### 4. ����ѹ����ļ����ƣ�ճ����ǰ����Ŀ��static/iconfont�ļ����£���pages/index.vue������iconfont����������
```
import '~/static/iconfont/iconfont.css'
```
#### 5. ��static�ļ������½�common.css�ļ���Ϊȫ����ʽ�ļ�����nuxt.config.js������ȫ����ʽ�ļ�����link���������{ rel: 'stylesheet' , type:'text/css' , href:'/common.css' };
������assets�ļ������½�common.css�ļ���Ϊȫ����ʽ�ļ�����nuxt.config.js������ȫ����ʽ�ļ�����css�����м���'~assets/css/common.css'

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
      <nuxt-link to="/">��ҳ</nuxt-link>
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
----index.vue
----author
------index.vue
----blog
------index.vue
----message
------index.vue
```

#### 7. ����sass������npm install --save-dev node-sass sass-loader��ʹ��<style lang="scss" scoped></style>

#### 8. ��װ���壬���������������ļ�˼Դ����.tof��˼Դ����.ttf��������static/font�ļ����У���common.css����������´���
```
@font-face
{
font-family: heiti;
src: url('~static/font/˼Դ����.otf'),
    url('~static/font/˼Դ����.ttf')
}
```

#### 9. �޸Ķ˿ںţ���nuxt.config.js��������´���
```
server:{
    port:8080,
    host:'0.0.0.0'
}
```

### 10. ����axios���������������⣬��װ����npm install @nuxtjs/axios @nuxtjs/axios --save����nuxt.config.js���������£�
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
### 11. �첽��������
```
//����һ
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

//��������ע��⹹��ֵ���÷�
  async asyncData (ctx) {
    const {count,data} = await ctx.$axios.$get('/api/blogs?page=1&limit=10')
    return { count:count, list:data }
  },

```

### 12. ·�ɴ��Σ�����Ҫ������ҳ������Ϊ��_������.vue������ʽ���粩������ҳ��Ŀ¼Ϊpages/blog/_blogId.vue��ҳ��·��Ϊ/blog/5d7eedf4dc115a1d84de6262����_blogId.vue���ȡ�������������ݴ�������
```
  async asyncData(ctx){
    const {data}=await ctx.$axios.$get('/api/blogs/checkDetail?blogId='+ctx.params.blogId);
    return {article:data};
  },
```
### 13. �������ȾӦ�ò�������npm run build��npm run start