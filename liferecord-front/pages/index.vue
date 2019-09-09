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

<style>

</style>
