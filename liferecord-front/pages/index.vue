<template>
  <div class="app">
    <menubar></menubar>
    <nuxt-child/>
  </div>
</template>
<script>
import menubar from '@/components/menubar.vue'
import '@/static/iconfont/iconfont.css'
export default {
  components: {
    menubar
  }
}
</script>

<style lang="scss">
.app{
  font-family: heiti;
  
}
</style>
