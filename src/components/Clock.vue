<template>
  <div class="all">
    <clock-view :clock-position="true"></clock-view>
    <clock-pannel></clock-pannel>
  </div>
</template>

<script>
import ClockView from './ClockView'
import ClockPannel from './ClockPannel'
export default {
  name: 'Clock',
  data () {
    return {
      appTitle: 'Vue 时钟',
      hour: '--',
      hourDeg: '0deg',
      mins: '--',
      minsDeg: '0deg',
      secs: '--',
      secsDeg: '0deg',
      hideClock: false
    }
  },
  created () {
    this.updateClock()
  },
  components: {
    ClockView,
    ClockPannel
  },
  methods: {
    updateClock () {
      var ctx = this
      setInterval(function () {
        var date = new Date()
        var hour = date.getHours()
        var min = date.getMinutes()
        var sec = date.getSeconds()
        // Set Display
        ctx.hour = (hour < 10) ? '0' + hour : hour
        ctx.mins = (min < 10) ? '0' + min : min
        ctx.secs = (sec < 10) ? '0' + sec : sec
        // Set Analog
        var analogHour = (hour > 12) ? hour - 12 : hour
        var analogMins = min
        var analogSecs = sec
        ctx.hourDeg = (analogHour * 30) + 'deg'
        ctx.minsDeg = (analogMins / 60 * 360) + 'deg'
        ctx.secsDeg = (analogSecs / 60 * 360) + 'deg'
      }, 1000)
    }
  }
}
</script>

<style>
.all {
  width: 100%;
}
</style>