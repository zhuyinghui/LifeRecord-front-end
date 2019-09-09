<template>
  <div class="container">
    <menubar></menubar>
    <nuxt-child/>
    <div style="width:1440px;height:50px;background:gold;">fff</div>
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

<style scoped>
.container{
  background: red;
}
</style>
