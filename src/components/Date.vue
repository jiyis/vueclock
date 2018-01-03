<template>
    <div id="config-date" class="section active">
        <div class="row">
            <h2 data-i18n="date">日期</h2>
        </div>
        <div class="row">
            <div class="input">
                <input id="set-date" class="toggle toggle-yes-no" type="checkbox" checked="Checked" @click="changeDate">
                <label for="set-date" data-on="ON" data-off="OFF"></label>
            </div>
            <div class="label">
                <span data-i18n="date">日期</span>
                <small data-i18n="dateDesc">在页面中央显示日期。</small>
            </div>
            <div class="preview">
                <b>Monday, January 1, 2017</b>
            </div>
        </div>
        <div class="row">
            <div class="input">
                <input id="set-day" class="toggle toggle-yes-no" type="checkbox" checked="Checked" @click="changeWeek">
                <label for="set-day" data-on="ON" data-off="OFF"></label>
            </div>
            <div class="label">
                <span data-i18n="day">星期</span>
                <small data-i18n="dayDesc">显示星期（仅当“简化”关闭时适用）。</small>
            </div>
            <div class="preview">
                <b>Monday,</b> January 1, 2017
            </div>
        </div>
        <div class="row">
            <div class="input">
                <input id="set-year" class="toggle toggle-yes-no" type="checkbox" checked="Checked"  @click="changeYear">
                <label for="set-year" data-on="ON" data-off="OFF"></label>
            </div>
            <div class="label">
                <span data-i18n="year">年份</span>
                <small data-i18n="yearDesc">在日期中显示年份。</small>
            </div>
            <div class="preview">
                Monday, January 1, <b>2017</b>
            </div>
        </div>
        <div class="row">
            <div class="input">
                <input id="set-shortdate" class="toggle toggle-yes-no" type="checkbox" @click="changeEasy">
                <label for="set-shortdate" data-on="ON" data-off="OFF"></label>
            </div>
            <div class="label">
                <span data-i18n="shortForm">简化</span>
                <small data-i18n="shortFormDesc">显示日期的简化形式。</small>
            </div>
            <div class="preview">
                <b>01/31/2016</b>
            </div>
        </div>
    </div>
</template>

<script>
import Bus from './bus.js'
export default {
  name: 'Date',
  data () {
    return {
      colorValue: '',
      fColorValue: '#3FA9F5',
      bColorValue: '#FFFFFF',
      displayPicker: false,
      showDate: true,
      showWeek: true,
      showYear: true,
      showEasy: true
    }
  },
  methods: {
    changeDate () {
      this.showDate = !this.showDate
      Bus.$emit('changeDate', this.showDate)
    },
    changeWeek () {
      this.showWeek = !this.showWeek
      Bus.$emit('changeWeek', this.showWeek)
    },
    changeYear () {
      this.showYear = !this.showYear
      Bus.$emit('changeYear', this.showYear)
    },
    changeEasy () {
      this.showEasy = !this.showEasy
      Bus.$emit('changeEasy', this.showEasy)
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
