<template>
    <div class="pannel">
        <div id="settings-toggle" @click="togglePannel">
            <!-- &#8801; -->
            <svg version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 128 128" style="enable-background:new 0 0 128 128;" xml:space="preserve">
                <rect x="24" y="80" class="st0" width="16" height="16"></rect>
                <rect x="40" y="64" class="st0" width="16" height="16"></rect>
                <rect x="56" y="48" class="st0" width="16" height="16"></rect>
                <rect x="72" y="64" class="st0" width="16" height="16"></rect>
                <rect x="88" y="80" class="st0" width="16" height="16"></rect>
            </svg>
        </div>

        <el-tabs class="tabs" v-model="activeName" @tab-click="handleClick" v-if="isCollapse">
            <el-tab-pane label="颜色" name="first"><color-tab></color-tab></el-tab-pane>
            <el-tab-pane label="时间" name="second"><time-tab></time-tab></el-tab-pane>
            <el-tab-pane label="日期" name="third"><date-tab></date-tab></el-tab-pane>
        </el-tabs>
    </div>
</template>

<script>
  import Bus from './bus.js'
  import ColorTab from './Color'
  import DateTab from './Date'
  import TimeTab from './Time'
  export default {
    name: 'ClockPannel',
    data () {
      return {
        isCollapse: false,
        activeName: 'first'
      }
    },
    components: {
      ColorTab,
      DateTab,
      TimeTab
    },
    methods: {
      handleOpen (key, keyPath) {
        console.log(key, keyPath)
      },
      handleClose (key, keyPath) {
        console.log(key, keyPath)
      },
      togglePannel () {
        this.isCollapse = !this.isCollapse
        Bus.$emit('trans', this.isCollapse)
      },
      handleClick (tab, event) {
        console.log(tab, event)
      }
    }
  }
</script>

<style>
    .pannel {
        position: fixed;
        left: auto;
        display: block;
        width: 550px;
        height: 100vh;
        top: 0;
        right: 0;
        bottom: 0;
        z-index: +1;
        transform: translateX(0);
    }
    .el-menu-vertical-demo:not(.el-menu--collapse) {
        width: 200px;
       
    }

    .on-settings-toggle #settings-toggle svg {
        opacity: 0.3;
        transition: opacity 0.3s;
    }
    #settings-toggle svg {
        width: auto;
        height: 36px;
        opacity: 0.5;
        transition: opacity 0.3s;
    }
    #settings-toggle {
        position: absolute;
        right: 0;
        top: 0;
        z-index: +1;
        padding: 10px;
        cursor: pointer;
        font-family: "Quicksand", sans-serif;
        font-size: 36px;
        transform: rotate(0deg) scale(1, 1);
        transition: transform 0.3s;
    }
    #settings-toggle svg .st0 {
        fill: black;
    }
    #settings-toggle:hover {
        transform: rotate(-90deg) scale(1.75, 1.75);
    }
    .tabs {
        height: 100vh;
        background: #202020;
        padding: 20px
    }
    .el-tabs__item {
        color: #adb8b8;
        font-size: 16px;
    }
    .el-tabs__item:hover {
        color: white;
    }
    .el-tabs__item.is-active {
        color: white;
    }
</style>
