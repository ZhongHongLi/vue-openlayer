<template>
  <div id="app">
    <router-view/>
    <Map />
  </div>
</template>


<script>
import Map from '../src/views/map'
export default {
  components:{
    Map
  }
}
</script>

<style lang="less">


</style>
