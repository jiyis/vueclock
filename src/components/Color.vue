<template>
    <div id="config-color" class="section active">
        <div class="row">
            <h2 data-i18n="customColor">自定义颜色</h2>
        </div>
        <div class="row">
            <div class="label">
                <span data-i18n="bg">背景颜色</span>
                <small data-i18n="bgDesc">页面背景的颜色。</small>
            </div>
            <div class="input">
                <input id="set-background" v-model="bColorValue" ref="bc" @change="publishBColor" type="color" value="#3FA9F5">
            </div>
            <div class="input input-text short">
                <input id="set-background-value" :value="bColorValue" type="text">
            </div>
        </div>
        <div class="row">
            <div class="label">
                <span data-i18n="fg">前景颜色</span>
                <small data-i18n="fgDesc">字体和图标的颜色。</small>
            </div>
            <div class="input">
                <input id="set-foreground" v-model="fColorValue" ref="fc"  @change="publishFColor" type="color" value="#3FA9F5">
            </div>
            <div class="input input-text short">
                <input id="set-foreground-value" :value="fColorValue" type="text">
            </div>
        </div>
        <div class="row">
            <h2 data-i18n="themes">主题</h2>
        </div>
        <div class="row" id="themes">
          <div class="input" v-for="index in 48" v-bind:key="index">
            <button class="theme" :id="'theme'+('000'+index).slice(-2)" @click="changeColor($event)"></button>
          </div>
        </div>
    </div>
</template>

<script>
import Bus from './bus.js'
export default {
  name: 'Color',
  data () {
    return {
      colorValue: '',
      fColorValue: '#3FA9F5',
      bColorValue: '#FFFFFF',
      displayPicker: false
    }
  },
  methods: {
    publishBColor () {
      Bus.$emit('changeBColor', this.$refs.bc.value)
    },
    publishFColor () {
      Bus.$emit('changeFColor', this.$refs.fc.value)
    },
    changeColor (event) {
      Bus.$emit('changeBColor', window.getComputedStyle(event.currentTarget, false).backgroundColor)
      Bus.$emit('changeFColor', window.getComputedStyle(event.currentTarget, false).color)
    }
  }
}
</script>

<style scoped lang="scss">
@import "../../static/scss/base.scss";
#themes {
    flex-wrap: wrap;
}
.row {
    position: relative;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    width: 100%;
    font-size: 17px;
    padding: 0 10px 0 0;
}
.row .input {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    flex-shrink: 0;
    height: 70px;
    padding: 0 0 0 10px;
}
.theme {
    width: 35px;
    height: 35px;
    font-size: 22px;
    display: block;
    text-decoration: none;
    text-align: center;
    text-align: center;
    vertical-align: middle;
    border: 0;
    box-shadow: 0 0 5px #000;
    margin: 0 10px;
    padding: 0 0 4px;
    border-radius: 50%;
    transition: transform 0.2s;
}
.theme:after {
    content: '{ }';
    display: block;
}

#themes {
  flex-wrap: wrap;
}

.theme {
  width: 35px;
  height: 35px;
  font-size: 22px;
  display: block;
  text-decoration: none;
  text-align: center;
  text-align: center;
  vertical-align: middle;
  border: 0;
  box-shadow: 0 0 5px rgba(0, 0, 0, 1);
  margin: 0 10px;
  padding: 0 0 4px;
  border-radius: 50%;
  transition: transform 0.2s;
  &:after {
    content: '{ }';
    display: block;
  }
  &:hover {
    transform: scale(1.7, 1.7);
  }
  &:focus {
    outline: 0;
  }
}

#theme01 {
  background: #FFFFFF;
  color: #000000 !important;
}

#theme02 {
  background: #FFFFFF;
  color: #7AC943 !important;
}

#theme03 {
  background: #FFFFFF;
  color: #00A99D !important;
}

#theme04 {
  background: #FFFFFF;
  color: #3FA9F5 !important;
}

#theme05 {
  background: #FFFFFF;
  color: #93278F !important;
}

#theme06 {
  background: #FFFFFF;
  color: #FF7BAC !important;
}

#theme07 {
  background: #FFFFFF;
  color: #FF1D25 !important;
}

#theme08 {
  background: #FFFFFF;
  color: #FF931E !important;
}

#theme09 {
  background: #000000;
  color: #FFFFFF !important;
}

#theme10 {
  background: #000000;
  color: #7AC943 !important;
}

#theme11 {
  background: #000000;
  color: #00A99D !important;
}

#theme12 {
  background: #000000;
  color: #3FA9F5 !important;
}

#theme13 {
  background: #000000;
  color: #93278F !important;
}

#theme14 {
  background: #000000;
  color: #FF7BAC !important;
}

#theme15 {
  background: #000000;
  color: #FF1D25 !important;
}

#theme16 {
  background: #000000;
  color: #FF931E !important;
}

#theme17 {
  background: #E6E6E6;
  color: #333333 !important;
}

#theme18 {
  background: #7AC943;
  color: #000000 !important;
}

#theme19 {
  background: #00A99D;
  color: #000000 !important;
}

#theme20 {
  background: #3FA9F5;
  color: #000000 !important;
}

#theme21 {
  background: #93278F;
  color: #000000 !important;
}

#theme22 {
  background: #FF7BAC;
  color: #000000 !important;
}

#theme23 {
  background: #FF1D25;
  color: #000000 !important;
}

#theme24 {
  background: #FF931E;
  color: #000000 !important;
}

#theme25 {
  background: #333333;
  color: #E6E6E6 !important;
}

#theme26 {
  background: #7AC943;
  color: #FFFFFF !important;
}

#theme27 {
  background: #00A99D;
  color: #FFFFFF !important;
}

#theme28 {
  background: #3FA9F5;
  color: #FFFFFF !important;
}

#theme29 {
  background: #93278F;
  color: #FFFFFF !important;
}

#theme30 {
  background: #FF7BAC;
  color: #FFFFFF !important;
}

#theme31 {
  background: #FF1D25;
  color: #FFFFFF !important;
}

#theme32 {
  background: #FF931E;
  color: #FFFFFF !important;
}

#theme33 {
  background: #BDCCD4;
  color: #534741 !important;
}

#theme34 {
  background: #E2EDC1;
  color: #00A055 !important;
}

#theme35 {
  background: #C9F2EE;
  color: #0000FF !important;
}

#theme36 {
  background: #C8EAF5;
  color: #00AEEF !important;
}

#theme37 {
  background: #D8D6EC;
  color: #702C8D !important;
}

#theme38 {
  background: #FCE3EE;
  color: #F190AC !important;
}

#theme39 {
  background: #EEDFAC;
  color: #534741 !important;
}

#theme40 {
  background: #FFFAC0;
  color: #F4783B !important;
}

#theme41 {
  background: #E1E9F2;
  color: #004080 !important;
}

#theme42 {
  background: #EAF3E0;
  color: #008080 !important;
}

#theme43 {
  background: #004040;
  color: #FFFFFF !important;
}

#theme44 {
  background: #0000FF;
  color: #FFFFFF !important;
}

#theme45 {
  background: #93278F;
  color: #FF931E !important;
}

#theme46 {
  background: #FAC8D3;
  color: #895881 !important;
}

#theme47 {
  background: #C1172C;
  color: #FFF200 !important;
}

#theme48 {
  background: #FF8040;
  color: #000000 !important;
}
.row {
  position: relative;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  width: 100%;
  font-size: 17px;
  padding: 0 10px 0 0;
}

.row .label {
  padding: 0 10px;
  flex-grow: 1;
  text-align: left;
  small {
    display: block;
    font-size: 70%;
    line-height: 1.4;
    font-weight: 400;
    opacity: 0.5;
  }
}

.preview-title {
  font-size: 14px;
  text-transform: uppercase;
  opacity: 0.5;
  &+.input {
    width: 90px;
  }
}

.row .preview {
  font-size: 14px;
  flex-shrink: 0;
  color: rgba(255, 255, 255, 0.4);
  font-weight: 400;
  b {
    font-weight: 700;
    color: rgba(63, 169, 245, 0.8);
  }
}

.toggle {
  position: absolute;
  margin-left: -9999px;
  visibility: hidden;
}

.toggle+label,
label.standalone {
  display: block;
  position: relative;
  cursor: pointer;
  outline: none;
  user-select: none;
  height: 100%;
}

.row .input {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  flex-shrink: 0;
  height: 70px;
  padding: 0 0 0 10px;
}

.row .input-text {
  width: 50%;
  input[type="text"] {
    height: 40px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    width: 100%;
    padding: 0 5px;
    font-size: 16px;
    color: white;
    background: #000;
  }
}

.row .input-select {
  width: 50%;
  select {
    height: 40px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    width: 100%;
    padding: 0 5px;
    font-size: 16px;
    color: white;
    background: #000;
  }
}

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
label.standalone.alt:before {
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

// Range Slider
input[type=range].range {
  -webkit-appearance: none;
  width: 65px;
  margin: 6.5px 0;
}

input[type=range].range:focus {
  outline: none;
}

input[type=range].range::-webkit-slider-runnable-track {
  width: 100%;
  height: 5px;
  cursor: pointer;
  box-shadow: 0px 0px 0px rgba(0, 0, 0, 0), 0px 0px 0px rgba(13, 13, 13, 0);
  background: $grey;
  border-radius: 0px;
  border: 0px solid rgba(0, 0, 0, 0);
}

input[type=range].range::-webkit-slider-thumb {
  box-shadow: 0px 0px 0px rgba(0, 0, 0, 0), 0px 0px 0px rgba(13, 13, 13, 0);
  border: 0px solid rgba(0, 0, 0, 0);
  height: 18px;
  width: 18px;
  border-radius: 0px;
  background: #3fa9f5;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -6.5px;
}

input[type=range].range:focus::-webkit-slider-runnable-track {
  // background: #d0d0d0;
}
// Color picker
input[type="color"] {
  -webkit-appearance: none;
  width: 40px;
  height: 40px;
  border: none;
  padding: 0;
}

input[type="color"]::-webkit-color-swatch-wrapper {
  padding: 0;
}

input[type="color"]::-webkit-color-swatch {
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.input-text.short {
  width: 25%;
}

</style>
