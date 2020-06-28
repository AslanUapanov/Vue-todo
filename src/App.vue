<template>
  <div id="app">
    <Home></Home>
  </div>
</template>
<script>
import Home from '@/views/Home'
export default {
  components: {
    Home
  }
}
</script>
<style lang="sass">
#app
  background-image: linear-gradient(to top, #fbc2eb 0%, #a6c1ee 100%)
  width: 100%
  min-height: 700px 
  font-family: Abel
@font-face
  font-family: Abel
  src: url('./assets/fonts/Abel-Regular.ttf')
</style>
