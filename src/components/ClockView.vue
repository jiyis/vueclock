<template>
<div>
  <div class="left" v-if="!hideClock && !showDigital">
    <div class="clock face" v-bind:class="{ active: transnlation }">
      <div class="steps" v-bind:style="{ color: frontColor }"><span class="number">12</span><span class="number-bottom">6</span></div>
      <div class="steps" v-bind:style="{ color: frontColor }"><span class="number">1</span><span class="number-bottom">7</span></div>
      <div class="steps" v-bind:style="{ color: frontColor }"><span class="number">2</span><span class="number-bottom">8</span></div>
      <div class="steps" v-bind:style="{ color: frontColor }"><span class="number">3</span><span class="number-bottom">9</span></div>
      <div class="steps" v-bind:style="{ color: frontColor }"><span class="number">4</span><span class="number-bottom">10</span></div>
      <div class="steps" v-bind:style="{ color: frontColor }"><span class="number">5</span><span class="number-bottom">11</span></div>
      <div class="brand">{{ appTitle }}</div>
      <div class="hour" v-bind:style="{transform: 'rotate(' + hourDeg + ')'}"> </div>
      <div class="min" v-bind:style="{transform: 'rotate(' + minsDeg + ')'}"></div>
      <div class="sec" v-if="showSecond" v-bind:style="{transform: 'rotate(' + secsDeg + ')'}"></div>
    </div>
  </div>
  <div v-if="!hideClock && showDigital" class="digital" v-bind:style="{ color: frontColor }" v-bind:class="{ active: transnlation }">
    {{ time }}
  </div>
  <div id="date" class="fadein" v-bind:class="{ active: transnlation }"  v-bind:style="{ color: frontColor }" v-if="showDate">
    <time v-bind:class="{ main:hideClock  }">{{ date }}</time>
    <div class="week"></div>
  </div>
  <div class="bottom" v-bind:class="{ active: transnlation }"  v-bind:style="{ color: frontColor }">
      <div id="additional-clocks">
          <div class="clock2 fadein" v-if="showSecondClock">
              <time id="display-clock2-time" datetime="00:00">
                  {{ secondZone }}
              </time>
              <span id="display-clock2-label" class="label"></span>
          </div>
          <div class="clock3 fadein" v-if="showThirdClock">
              <time id="display-clock3-time" datetime="00:00">
                  {{ thirdZone }}
              </time>
              <span id="display-clock3-label" class="label"></span>
          </div>
          <div class="clock4 fadein" v-if="showFourthClock">
              <time id="display-clock4-time" datetime="00:00">
                  {{ fourthZone }}
              </time>
              <span id="display-clock4-label" class="label"></span>
          </div>
      </div>
  </div>
</div>
</template>


<script>
import Bus from './bus.js'
import moment from 'moment'
import momentZone from 'moment-timezone'
export default {
  name: 'ClockView',
  data: function () {
    return {
      appTitle: 'Vue 时钟',
      hour: '--',
      hourDeg: '0deg',
      mins: '--',
      minsDeg: '0deg',
      secs: '--',
      secsDeg: '0deg',
      transnlation: false,
      frontColor: '#3FA9F5',
      date: '',
      time: '',
      hideClock: false,
      showDate: true,
      showWeek: true,
      showYear: true,
      showEasy: true,
      showDigital: false,
      showSecond: true,
      showAM: false,
      showDelimiter: true,
      showSecondClock: true,
      showThirdClock: true,
      showFourthClock: true,
      secondZone: '',
      thirdZone: '',
      fourthZone: ''
    }
  },
  created () {
    this.updateClock()
    this.updateDate()
  },
  mounted () {
    Bus.$on('trans', (e) => {
      this.transnlation = e
    })
    Bus.$on('changeFColor', (e) => {
      this.frontColor = e
    })
    Bus.$on('changeClock', (e) => {
      this.hideClock = e
    })
    Bus.$on('changeDate', (e) => {
      this.showDate = e
    })
    Bus.$on('changeWeek', (e) => {
      this.showWeek = e
      this.updateDate()
    })
    Bus.$on('changeYear', (e) => {
      this.showYear = e
      this.updateDate()
    })
    Bus.$on('changeEasy', (e) => {
      this.showEasy = e
      this.updateDate()
    })
    Bus.$on('changeClockStyle', (e) => {
      this.showDigital = e
      this.updateTime()
    })
    Bus.$on('changeClockSecond', (e) => {
      this.showSecond = e
      this.updateTime()
    })
    Bus.$on('changeAM', (e) => {
      this.showAM = e
      this.updateTime()
    })
    Bus.$on('changeDelimiter', (e) => {
      this.showDelimiter = e
      this.updateTime()
    })
    Bus.$on('changeSecondClock', (e, zone) => {
      this.showSecondClock = e
      this.secondZone = momentZone().tz(zone).format('HH:mm') + ' ' + zone
    })
    Bus.$on('changeThirdClock', (e, zone) => {
      this.showThirdClock = e
      this.thirdZone = momentZone().tz(zone).format('HH:mm') + ' ' + zone
    })
    Bus.$on('changeFourthClock', (e, zone) => {
      this.showFourthClock = e
      this.fourthZone = momentZone().tz(zone).format('HH:mm') + ' ' + zone
    })
    Bus.$on('changeSecondClockZone', (e) => {
      this.secondZone = momentZone().tz(e).format('HH:mm') + ' ' + e
    })
    Bus.$on('changeThirdClockZone', (e) => {
      this.thirdZone = momentZone().tz(e).format('HH:mm') + ' ' + e
    })
    Bus.$on('changeFourthClockZone', (e) => {
      this.fourthZone = momentZone().tz(e).format('HH:mm') + ' ' + e
    })
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
    },
    updateTime () {
      var ctx = this
      setInterval(function () {
        let cd = new Date()
        let delimiter = ctx.showDelimiter ? ':' : ' '
        let hours = cd.getHours() > 12 ? 'pm' : 'am'
        let am = ctx.showAM ? ' ' + hours : ''
        let second = ctx.showSecond ? delimiter + ctx.zeroPadding(cd.getSeconds()) : ''
        ctx.time = ctx.zeroPadding(cd.getHours()) + delimiter + ctx.zeroPadding(cd.getMinutes()) + second + am
      }, 1000)
      let cd = new Date()
      let delimiter = ctx.showDelimiter ? ':' : ' '
      let hours = cd.getHours() > 12 ? 'pm' : 'am'
      let am = this.showAM ? ' ' + hours : ''
      let second = this.showSecond ? delimiter + this.zeroPadding(cd.getSeconds()) : '' + am
      this.time = this.zeroPadding(cd.getHours()) + delimiter + this.zeroPadding(cd.getMinutes()) + second
    },
    updateDate () {
      let week = ['星期天', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六']
      let month = ['一月', '二月', '三月', '四月', '五月', '六月', '七月', '八月', '九月', '十月', '十一月', '十二月']
      let cd = new Date()
      let weekValue = this.showWeek ? week[cd.getDay()] + ', ' : ''
      let yearValue = this.showYear ? ', ' + this.zeroPadding(cd.getFullYear(), 4) : ''
      if (this.showEasy) {
        this.date = weekValue + month[cd.getMonth()] + ' ' + cd.getDate() + yearValue
      } else {
        this.date = weekValue + moment().format('YYYY/MM/DD')
      }
    },
    zeroPadding (num, digit) {
      var zero = ''
      for (var i = 0; i < digit; i++) {
        zero += '0'
      }
      return (zero + num).slice(-digit)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "../../static/scss/base.scss";
.left {
    position: relative;
    width: 100vw;
    padding-bottom: 30px;
    overflow: hidden;
    display: flex;
}
.clock{
  position: relative;
  width: 400px;
  height: 400px;
  border-radius: 50%;
  margin: 0 auto;
  &::before{
    z-index: 3;
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    width: 20px;
    height: 20px;
    transform: translate(-50%, -50%);
    background: $clock-col;
    border-radius: 50%;
  }
  .steps{
    position: absolute;
    top: 0;
    left: 50%;
    margin-left: -2px;
    height: 100%;
    width: 4px;
    &::before, &::after{
      /*content: '';*/
      position: absolute;
      left: -3px;
      width: 10px;
      height: 10px;
      border-radius: 50%;
    }
    &::before{
      top: .5rem;
    }
    &::after{
      bottom: .5rem;
    }
    &:nth-child(1){
      &::before, &::after{
        background: $accent-col;
      }
    }
    &:nth-child(2){ 
      transform: rotate(30deg); 
      .number {
        transform: rotate(330deg); 
      }
      .number-bottom {
        transform: rotate(330deg); 
      }
    }
    &:nth-child(3){ 
      transform: rotate(60deg); 
      .number {
        transform: rotate(300deg); 
      }
      .number-bottom {
        transform: rotate(300deg); 
      }
    }
    &:nth-child(4){ 
      transform: rotate(90deg);
      &::before, &::after{
        background: $accent-col;
      }
      .number {
        transform: rotate(270deg); 
      }
      .number-bottom {
        transform: rotate(270deg); 
      }
    }
    &:nth-child(5){
      transform: rotate(120deg); 
      .number {
        transform: rotate(240deg); 
      }
      .number-bottom {
        transform: rotate(240deg); 
      }
    }
    &:nth-child(6){ 
      transform: rotate(150deg); 
      .number {
        transform: rotate(210deg); 
      }
      .number-bottom {
        transform: rotate(210deg); 
      }
    }
  }
 .number {
    position: absolute;
    top: 22px;
    left: -6px;
    font-size: 18px;
  }
  .number-bottom {
    position: absolute;
    bottom: 22px;
    left: -2px;
    font-size: 18px;
  }
  .brand{
    position: absolute;
    bottom: 5rem;
    left: 50%;
    transform: translateX(-50%);
    font-family: $font-text;
    text-transform: uppercase;
    font-size: .85em;
    opacity: .5;
    color: #000; 
  }
  .display{
    position: absolute;
    top: 6rem;
    left: 50%;
    transform: translateX(-50%);
    font-family: $font-display;
    font-size: 2.6em;
    opacity: .5;
  }
  .hour,
  .min,
  .sec{
    z-index: 2;
    position: absolute;
    bottom: 50%;
    left: 50%;
    height: 40%;
    width: 4px;
    margin-left: -2px;
    background: $accent-col;
    transform-origin: bottom center;
    border-radius: 3px 3px 0 0;
  }
  .hour{
    height: 30%;
  }
  .sec{
    z-index: 1;
    height: 46%;
    background: $clock-col;
  }
}
.face{
  position: relative;
  /* background: #eee; */
  /* background-image: -webkit-gradient(linear, left top, right bottom, from(#eee), to(#f5f5f5)); */
  /*background-image: linear-gradient(to bottom right, #4134b6, #f5f5f5);*/
  padding: 0px;
  border-radius: 50%;
  border: 15px solid #d9d9d9;
  -webkit-box-shadow: 20px 20px 30px -10px rgba(143, 73, 73, 0.4), inset 10px 10px 20px rgba(0, 0, 0, 0.2);
  box-shadow: 20px 20px 30px -10px rgba(0, 0, 0, 0.4), inset 10px 10px 20px rgba(0, 0, 0, 0.2);
}
@media screen and (max-width: 480px){
  .clock{
    width: 300px;
    height: 300px;
    .brand{
      bottom: 3rem;
    }
    .display{
      top: 4.5rem;
      font-size: 2.2em;
    }
  }
}
.clock.active, #date.active, .digital.active, .bottom.active {
    transform: translateX(-280px);
}
#date {
    display: block;
    font-size: 40px;
    line-height: 1;
    margin-bottom: 0em;
}
.main {
  font-size: 80px !important;
}
.main::before {
  content: '{';
  padding: 0 30px;
}
.main::after {
  content: '}';
  padding: 0 30px;
}
.digital {
  font-size: 130px !important;
}
.digital::before {
  content: '{';
  padding: 0 30px;
}
.digital::after {
  content: '}';
  padding: 0 30px;
}
#additional-clocks {
  display: flex;
  justify-content: center;
  align-content: flex-start;
  text-align: center;
  padding: 0.02em 0 0 0;
  &>div {
    padding: 0 .05em;
  }
  time {
    font-size: 26px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: 300;
    line-height: 1;
    .meridiem {
      font-size: 40%;
      margin-left: 0.2em;
    }
  }
  .label {
    display: block;
    font-size: 1.3%;
    font-weight: 700;
    line-height: 1;
    margin-top: 0.3em;
  }
  .delimiter {
    opacity: 0;
  }
}

.on-delimiter {
  #additional-clocks .delimiter {
    opacity: 1;
  }
}

.on-delimiter.on-dimdelimiter {
  #additional-clocks .delimiter {
    opacity: 0.5;
  }
}

.on-military {
  #additional-clocks .meridiem {
    display: none;
  }
}

.on-clock2 #additional-clocks .clock2 {
  display: block;
}

.on-clock3 #additional-clocks .clock3 {
  display: block;
}

.on-clock4 #additional-clocks .clock4 {
  display: block;
}

// Special Cases
.font-exo-2 #additional-clocks {
  .delimiter {
    margin-bottom: 0.25em;
  }
}

.font-quicksand #additional-clocks {
  .delimiter {
    margin-bottom: 0.15em;
  }
}

.font-press-start-2p #additional-clocks {
  time {
    font-size: 4.0%;
  }
  .label {
    font-size: 1.2%;
  }
}
#additional-clocks > div {
  padding:  .5em;
}
</style>