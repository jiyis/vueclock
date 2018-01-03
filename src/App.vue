<template>
  <div id="app" v-bind:style="{ background: backgroundColor }">
    <router-view/>
  </div>
</template>

<script>
import Bus from './components/bus.js'
export default {
  name: 'app',
  data () {
    return {
      backgroundColor: '#FFFFFF'
    }
  },
  mounted () {
    Bus.$on('changeBColor', (e) => {
      this.backgroundColor = e
    })
  }

}
</script>

<style lang="scss">
@import "../static/scss/base.scss";
#app{
  min-height: 100vh;
  color: $clock-col;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
