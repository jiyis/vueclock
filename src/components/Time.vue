<template>
    <div id="config-time" class="section active">
        <div class="row">
            <h2 data-i18n="primaryClock">主时钟</h2>
        </div>
        <div class="row">
            <div class="input">
                <input id="set-clock1" class="toggle toggle-yes-no" type="checkbox" checked="Checked" @click="changeClock">
                <label for="set-clock1" data-on="ON" data-off="OFF"></label>
            </div>
            <div class="label">
                <span data-i18n="primaryClock">主时钟</span>
                <small data-i18n="primaryClockDesc">在页面中央显示主时钟。</small>
            </div>
            <div class="preview">
                <b>12:00:00 AM</b>
            </div>
        </div>
        <div class="row">
            <div class="input">
                <input id="set-analog" class="toggle toggle-yes-no" type="checkbox" @click="changeClockStyle">
                <label for="set-analog" data-on="DIGITAL" data-off="ANALOG" class="alt"></label>
            </div>
            <div class="label">
                <span data-i18n="clockStyle">时钟样式</span>
                <small data-i18n="clockStyleDesc">在数码时钟和模拟时钟之间切换（使用模拟时钟时括号会被隐藏）。</small>
            </div>
            <div class="preview">
                &nbsp;
            </div>
        </div>
        <div class="row">
            <div class="input">
                <input id="set-seconds" class="toggle toggle-yes-no" type="checkbox" checked="Checked" @click="changeClockSecond">
                <label for="set-seconds" data-on="ON" data-off="OFF"></label>
            </div>
            <div class="label">
                <span data-i18n="seconds">秒数</span>
                <small data-i18n="secondsDesc">显示主时钟的秒数。</small>
            </div>
            <div class="preview">
                12:00<b>:00</b> AM
            </div>
        </div>
        <div class="row">
            <div class="input">
                <input id="set-meridiem" class="toggle toggle-yes-no" type="checkbox" @click="changeAM">
                <label for="set-meridiem" data-on="ON" data-off="OFF"></label>
            </div>
            <div class="label">
                <span data-i18n="meridiem">上午/下午</span>
                <small data-i18n="meridiemDesc">在主时钟显示上午/下午。</small>
            </div>
            <div class="preview">
                12:00:00 <b>AM</b>
            </div>
        </div>
        <div class="row">
            <div class="input">
                <input id="set-delimiter" class="toggle toggle-yes-no" type="checkbox" checked="Checked" @click="changeDelimiter">
                <label for="set-delimiter" data-on="ON" data-off="OFF"></label>
            </div>
            <div class="label">
                <span data-i18n="delimiter">分隔符</span>
                <small data-i18n="delimiterDesc">在所有时钟的时间之间显示分隔符。</small>
            </div>
            <div class="preview">
                12<b>:</b>00<b>:</b>00 AM
            </div>
        </div>
        <div class="row">
            <h2 data-i18n="additionalClocks">附加时钟</h2>
        </div>
        <div class="row">
            <div class="input">
                <input id="set-time2" class="toggle toggle-yes-no" type="checkbox" @click="changeSecondClock">
                <label for="set-time2" data-on="ON" data-off="OFF"></label>
            </div>
            <div class="label">
                <span data-i18n="secondClock">第二个时钟</span>
                <small data-i18n="secondClockDesc">在主时钟下面显示一个额外的时钟。</small>
            </div>
        </div>
        <div id="clock2-timezone" class="row" v-if="showSecondClock">
            <div class="label">
                <span data-i18n="secondClockTimezone">第二个时钟的时区</span>
                <small data-i18n="secondClockTimezoneDesc">选择这个时钟的时区。</small>
            </div>
            <div class="input input-select">
                <select id="set-time2-zone" class="timezones"  v-model="secondZone" @change="changeSecondClockZone">  <option value="Pacific/Midway">(GMT -11:00) Midway Island, Samoa</option>  <option value="Pacific/Honolulu">(GMT -10:00) Hawaii</option>  <option value="America/Anchorage">(GMT -9:00) Alaska</option>  <option value="America/Los_Angeles">(GMT -8:00) Pacific Time (US &amp; Canada)</option>  <option value="America/Boise">(GMT -7:00) Mountain Time (US &amp; Canada)</option>  <option value="America/Phoenix">(GMT -7:00) Mountain Standard Time (US &amp; Canada), America/Phoenix</option>  <option value="America/Chicago">(GMT -6:00) Central Time (US &amp; Canada), Mexico City</option>  <option value="America/Belize">(GMT -6:00) Central Standard Time (America), Belize, Costa Rica</option>  <option value="America/New_York">(GMT -5:00) Eastern Time (US &amp; Canada), Bogota, Lima</option>  <option value="Atlantic/Bermuda">(GMT -4:00) Atlantic Time (Canada), Canada/Atlantic</option>  <option value="Canada/Newfoundland">(GMT -3:30) Newfoundland</option>  <option value="America/Argentina/Buenos_Aires">(GMT -3:00) Brazil, Buenos Aires, Georgetown</option>  <option value="Atlantic/South_Georgia">(GMT -2:00) Mid-Atlantic</option>  <option value="Atlantic/Azores">(GMT -1:00 hour) Azores, Cape Verde Islands</option>  <option value="Europe/London">(GMT) Western Europe Time, London, Lisbon, Casablanca</option>  <option value="Europe/Paris">(GMT +1:00 hour) Brussels, Copenhagen, Madrid, Paris</option>  <option value="Europe/Kaliningrad">(GMT +2:00) Kaliningrad, South Africa</option>  <option value="Asia/Baghdad">(GMT +3:00) Baghdad, Riyadh, Moscow, St. Petersburg</option>  <option value="Asia/Tehran">(GMT +3:30) Tehran</option>  <option value="Asia/Muscat">(GMT +4:00) Abu Dhabi, Muscat, Baku, Tbilisi</option>  <option value="Asia/Kabul">(GMT +4:30) Kabul</option>  <option value="Asia/Karachi">(GMT +5:00) Ekaterinburg, Islamabad, Karachi, Tashkent</option>  <option value="Asia/Calcutta">(GMT +5:30) Bombay, Calcutta, Madras, New Delhi</option>  <option value="Asia/Kathmandu">(GMT +5:45) Kathmandu</option>  <option value="Asia/Almaty">(GMT +6:00) Almaty, Dhaka, Colombo</option>  <option value="Asia/Bangkok">(GMT +7:00) Bangkok, Hanoi, Jakarta</option>  <option value="Asia/Hong_Kong">(GMT +8:00) Beijing, Perth, Singapore, Hong Kong</option>  <option value="Asia/Tokyo">(GMT +9:00) Tokyo, Seoul, Osaka, Sapporo, Yakutsk</option>  <option value="Australia/Adelaide">(GMT +9:30) Adelaide, Darwin</option>  <option value="Pacific/Guam">(GMT +10:00) Eastern Australia, Guam, Vladivostok</option>  <option value="Asia/Magadan">(GMT +11:00) Magadan, Solomon Islands, New Caledonia</option>  <option value="Pacific/Auckland">(GMT +12:00) Auckland, Wellington, Fiji, Kamchatka</option>  </select>
            </div>
        </div>
        <div class="row">
            <div class="input">
                <input id="set-time3" class="toggle toggle-yes-no" type="checkbox" @click="changeThirdClock">
                <label for="set-time3" data-on="ON" data-off="OFF"></label>
            </div>
            <div class="label">
                <span data-i18n="thirdClock">第三个时钟</span>
                <small data-i18n="thirdClockDesc">在主时钟下面显示一个额外的时钟。</small>
            </div>
        </div>
        <div id="clock3-timezone" class="row" v-if="showThirdClock">
            <div class="label">
                <span data-i18n="thirdClockTimezone">第三个时钟的时区</span>
                <small data-i18n="thirdClockTimezoneDesc">选择这个时钟的时区。</small>
            </div>
            <div class="input input-select">
                <select id="set-time3-zone" class="timezones" v-model="thirdZone" @change="changeThirdClockZone">  <option value="Pacific/Midway">(GMT -11:00) Midway Island, Samoa</option>  <option value="Pacific/Honolulu">(GMT -10:00) Hawaii</option>  <option value="America/Anchorage">(GMT -9:00) Alaska</option>  <option value="America/Los_Angeles">(GMT -8:00) Pacific Time (US &amp; Canada)</option>  <option value="America/Boise">(GMT -7:00) Mountain Time (US &amp; Canada)</option>  <option value="America/Phoenix">(GMT -7:00) Mountain Standard Time (US &amp; Canada), America/Phoenix</option>  <option value="America/Chicago">(GMT -6:00) Central Time (US &amp; Canada), Mexico City</option>  <option value="America/Belize">(GMT -6:00) Central Standard Time (America), Belize, Costa Rica</option>  <option value="America/New_York">(GMT -5:00) Eastern Time (US &amp; Canada), Bogota, Lima</option>  <option value="Atlantic/Bermuda">(GMT -4:00) Atlantic Time (Canada), Canada/Atlantic</option>  <option value="Canada/Newfoundland">(GMT -3:30) Newfoundland</option>  <option value="America/Argentina/Buenos_Aires">(GMT -3:00) Brazil, Buenos Aires, Georgetown</option>  <option value="Atlantic/South_Georgia">(GMT -2:00) Mid-Atlantic</option>  <option value="Atlantic/Azores">(GMT -1:00 hour) Azores, Cape Verde Islands</option>  <option value="Europe/London">(GMT) Western Europe Time, London, Lisbon, Casablanca</option>  <option value="Europe/Paris">(GMT +1:00 hour) Brussels, Copenhagen, Madrid, Paris</option>  <option value="Europe/Kaliningrad">(GMT +2:00) Kaliningrad, South Africa</option>  <option value="Asia/Baghdad">(GMT +3:00) Baghdad, Riyadh, Moscow, St. Petersburg</option>  <option value="Asia/Tehran">(GMT +3:30) Tehran</option>  <option value="Asia/Muscat">(GMT +4:00) Abu Dhabi, Muscat, Baku, Tbilisi</option>  <option value="Asia/Kabul">(GMT +4:30) Kabul</option>  <option value="Asia/Karachi">(GMT +5:00) Ekaterinburg, Islamabad, Karachi, Tashkent</option>  <option value="Asia/Calcutta">(GMT +5:30) Bombay, Calcutta, Madras, New Delhi</option>  <option value="Asia/Kathmandu">(GMT +5:45) Kathmandu</option>  <option value="Asia/Almaty">(GMT +6:00) Almaty, Dhaka, Colombo</option>  <option value="Asia/Bangkok">(GMT +7:00) Bangkok, Hanoi, Jakarta</option>  <option value="Asia/Hong_Kong">(GMT +8:00) Beijing, Perth, Singapore, Hong Kong</option>  <option value="Asia/Tokyo">(GMT +9:00) Tokyo, Seoul, Osaka, Sapporo, Yakutsk</option>  <option value="Australia/Adelaide">(GMT +9:30) Adelaide, Darwin</option>  <option value="Pacific/Guam">(GMT +10:00) Eastern Australia, Guam, Vladivostok</option>  <option value="Asia/Magadan">(GMT +11:00) Magadan, Solomon Islands, New Caledonia</option>  <option value="Pacific/Auckland">(GMT +12:00) Auckland, Wellington, Fiji, Kamchatka</option>  </select>
            </div>
        </div>
        <div class="row">
            <div class="input">
                <input id="set-time4" class="toggle toggle-yes-no" type="checkbox"  @click="changeFourthClock">
                <label for="set-time4" data-on="ON" data-off="OFF"></label>
            </div>
            <div class="label">
                <span data-i18n="fourthClock">第四个时钟</span>
                <small data-i18n="fourthClockDesc">在主时钟下面显示一个额外的时钟。</small>
            </div>
        </div>
        <div id="clock4-timezone" class="row" v-if="showFourthClock">
            <div class="label">
                <span data-i18n="fourthClockTimezone">第四个时钟的时区</span>
                <small data-i18n="fourthClockTimezoneDesc">选择这个时钟的时区。</small>
            </div>
            <div class="input input-select">
                <select id="set-time4-zone" v-model="fourthZone" @change="changeFourthClockZone" class="timezones" >  <option value="Pacific/Midway">(GMT -11:00) Midway Island, Samoa</option>  <option value="Pacific/Honolulu">(GMT -10:00) Hawaii</option>  <option value="America/Anchorage">(GMT -9:00) Alaska</option>  <option value="America/Los_Angeles">(GMT -8:00) Pacific Time (US &amp; Canada)</option>  <option value="America/Boise">(GMT -7:00) Mountain Time (US &amp; Canada)</option>  <option value="America/Phoenix">(GMT -7:00) Mountain Standard Time (US &amp; Canada), America/Phoenix</option>  <option value="America/Chicago">(GMT -6:00) Central Time (US &amp; Canada), Mexico City</option>  <option value="America/Belize">(GMT -6:00) Central Standard Time (America), Belize, Costa Rica</option>  <option value="America/New_York">(GMT -5:00) Eastern Time (US &amp; Canada), Bogota, Lima</option>  <option value="Atlantic/Bermuda">(GMT -4:00) Atlantic Time (Canada), Canada/Atlantic</option>  <option value="Canada/Newfoundland">(GMT -3:30) Newfoundland</option>  <option value="America/Argentina/Buenos_Aires">(GMT -3:00) Brazil, Buenos Aires, Georgetown</option>  <option value="Atlantic/South_Georgia">(GMT -2:00) Mid-Atlantic</option>  <option value="Atlantic/Azores">(GMT -1:00 hour) Azores, Cape Verde Islands</option>  <option value="Europe/London">(GMT) Western Europe Time, London, Lisbon, Casablanca</option>  <option value="Europe/Paris">(GMT +1:00 hour) Brussels, Copenhagen, Madrid, Paris</option>  <option value="Europe/Kaliningrad">(GMT +2:00) Kaliningrad, South Africa</option>  <option value="Asia/Baghdad">(GMT +3:00) Baghdad, Riyadh, Moscow, St. Petersburg</option>  <option value="Asia/Tehran">(GMT +3:30) Tehran</option>  <option value="Asia/Muscat">(GMT +4:00) Abu Dhabi, Muscat, Baku, Tbilisi</option>  <option value="Asia/Kabul">(GMT +4:30) Kabul</option>  <option value="Asia/Karachi">(GMT +5:00) Ekaterinburg, Islamabad, Karachi, Tashkent</option>  <option value="Asia/Calcutta">(GMT +5:30) Bombay, Calcutta, Madras, New Delhi</option>  <option value="Asia/Kathmandu">(GMT +5:45) Kathmandu</option>  <option value="Asia/Almaty">(GMT +6:00) Almaty, Dhaka, Colombo</option>  <option value="Asia/Bangkok">(GMT +7:00) Bangkok, Hanoi, Jakarta</option>  <option value="Asia/Hong_Kong">(GMT +8:00) Beijing, Perth, Singapore, Hong Kong</option>  <option value="Asia/Tokyo">(GMT +9:00) Tokyo, Seoul, Osaka, Sapporo, Yakutsk</option>  <option value="Australia/Adelaide">(GMT +9:30) Adelaide, Darwin</option>  <option value="Pacific/Guam">(GMT +10:00) Eastern Australia, Guam, Vladivostok</option>  <option value="Asia/Magadan">(GMT +11:00) Magadan, Solomon Islands, New Caledonia</option>  <option value="Pacific/Auckland">(GMT +12:00) Auckland, Wellington, Fiji, Kamchatka</option>  </select>
            </div>
        </div>
        <div class="row">
            <p><small data-i18n="timeDisclaimer"><b>注意</b> 主时钟和附加时钟显示的时间是基于您的电脑设置的时间和时区。对于您所在时区的检测基本上是有根据的猜测，可能不会反映您的真实时区，这会导致附加时钟的时间被关闭。现在 CaretTab 检测您的所在时区为：</small><small> "<span id="current-timezone">Asia/Shanghai</span>"</small></p>
        </div>
    </div>
</template>

<script>
import Bus from './bus.js'
export default {
  name: 'Time',
  data () {
    return {
      colorValue: '',
      fColorValue: '#3FA9F5',
      bColorValue: '#FFFFFF',
      displayPicker: false,
      hideClock: false,
      showDigital: false,
      showSecond: true,
      showAM: false,
      showDelimiter: true,
      showSecondClock: false,
      showThirdClock: false,
      showFourthClock: false,
      secondZone: 'America/Anchorage',
      thirdZone: 'Pacific/Honolulu',
      fourthZone: 'Pacific/Midway'
    }
  },
  methods: {
    changeClock () {
      this.hideClock = !this.hideClock
      Bus.$emit('changeClock', this.hideClock)
    },
    changeClockStyle () {
      this.showDigital = !this.showDigital
      Bus.$emit('changeClockStyle', this.showDigital)
    },
    changeClockSecond () {
      this.showSecond = !this.showSecond
      Bus.$emit('changeClockSecond', this.showSecond)
    },
    changeAM () {
      this.showAM = !this.showAM
      Bus.$emit('changeAM', this.showAM)
    },
    changeDelimiter () {
      this.showDelimiter = !this.showDelimiter
      Bus.$emit('changeDelimiter', this.showDelimiter)
    },
    changeSecondClock () {
      this.showSecondClock = !this.showSecondClock
      Bus.$emit('changeSecondClock', this.showSecondClock, this.secondZone)
    },
    changeThirdClock () {
      this.showThirdClock = !this.showThirdClock
      Bus.$emit('changeThirdClock', this.showThirdClock, this.thirdZone)
    },
    changeFourthClock () {
      this.showFourthClock = !this.showFourthClock
      Bus.$emit('changeFourthClock', this.showFourthClock, this.fourthZone)
    },
    changeSecondClockZone () {
      Bus.$emit('changeSecondClockZone', this.showSecondClock)
    },
    changeThirdClockZone () {
      Bus.$emit('changeThirdClockZone', this.showThirdClock)
    },
    changeFourthClockZone () {
      Bus.$emit('changeFourthClockZone', this.fourthZone)
    }
  }
}
</script>

<style scoped lang="scss">
@import "../../static/scss/base.scss";
// Toggle button
input.toggle-yes-no+label,
label.standalone {
  flex-shrink: 0;
  width: 65px;
  height: 34px;
  &.sm {
    width: 34px;
    &:before,
    &:after {
      font-size: 26px;
    }
    &.brackets-toggle:before,
    &.brackets-toggle:after,
    &.date-delimiter-toggle:before,
    &.date-delimiter-toggle:after {
      line-height: 30px;
    }
  }
}

input.toggle-yes-no+label:before,
input.toggle-yes-no+label:after,
label.standalone:before,
label.standalone:after {
  display: block;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  color: #fff;
  font-size: 16px;
  text-align: center;
  line-height: 34px;
}

input.toggle-yes-no+label.alt:before,
input.toggle-yes-no+label.alt:after,
label.standalone:before,
label.standalone:after {
  font-size: 14px;
}

input.toggle-yes-no+label:before,
label.standalone:before {
  background-color: $grey;
  content: attr(data-off);
  transition: transform 0.5s;
  backface-visibility: hidden;
}

input.toggle-yes-no+label.alt:before,
label.standalone.alt:before
input.toggle-yes-no+label,
label.standalone {
  flex-shrink: 0;
  width: 65px;
  height: 34px;
  &.sm {
    width: 34px;
    &:before,
    &:after {
      font-size: 26px;
    }
    &.brackets-toggle:before,
    &.brackets-toggle:after,
    &.date-delimiter-toggle:before,
    &.date-delimiter-toggle:after {
      line-height: 30px;
    }
  }
}

input.toggle-yes-no+label:before,
input.toggle-yes-no+label:after,
label.standalone:before,
label.standalone:after {
  display: block;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  color: #fff;
  font-size: 16px;
  text-align: center;
  line-height: 34px;
}

input.toggle-yes-no+label.alt:before,
input.toggle-yes-no+label.alt:after,
label.standalone:before,
label.standalone:after {
  font-size: 14px;
}

input.toggle-yes-no+label:before,
label.standalone:before {
  background-color: $grey;
  content: attr(data-off);
  transition: transform 0.5s;
  backface-visibility: hidden;
}

e {
  background-color: $blue;
}

input.toggle-yes-no+label:after,
label.standalone:after {
  background-color: $green;
  content: attr(data-on);
  transition: transform 0.5s;
  transform: rotateY(180deg);
  backface-visibility: hidden;
}

input.toggle-yes-no:checked+label:before,
label.standalone:before {
  transform: rotateY(180deg);
}

input.toggle-yes-no:checked+label:after,
label.standalone:after {
  transform: rotateY(0);
}

</style>
