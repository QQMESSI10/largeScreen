<template>
  <div class="home">
    <div class="top">
      <img src="./assets/top2.png" />
      <div class="top-title">滕州-天气视图</div>
    </div>
    <div class="left">
      <div class="module left-top">
        <div class="module-title">
          <span>实时天气</span>
        </div>
        <LeftTop v-if="showCharts" :observe="observe" :tips="tips"/>
        <span class="line line-top"></span>
        <span class="line line-right"></span>
        <span class="line line-bottom"></span>
        <span class="line line-left"></span>
      </div>
      <div class="module left-center">
        <div class="module-title">
          <span>空气质量</span>
        </div>
        <LeftCenter v-if="showCharts" :air="air"/>
        <span class="line line-top"></span>
        <span class="line line-right"></span>
        <span class="line line-bottom"></span>
        <span class="line line-left"></span>
      </div>
      <div class="module left-bottom">
        <div class="module-title">
          <span>今日建议</span>
        </div>
        <LeftBottom v-if="showCharts" :indexTips="indexTips"/>
        <span class="line line-top"></span>
        <span class="line line-right"></span>
        <span class="line line-bottom"></span>
        <span class="line line-left"></span>
      </div>
    </div>
    <div class="center">
      <Center v-if="showCharts" :alarm="alarm"/>
    </div>
    <div class="right">
      <div class="module right-top">
        <div class="module-title">
          <span>未来气温情况</span>
        </div>
        <RightTop v-if="showCharts" :forecast_24h="forecast_24h"/>
        <span class="line line-top"></span>
        <span class="line line-right"></span>
        <span class="line line-bottom"></span>
        <span class="line line-left"></span>
      </div>
      <div class="module right-center">
        <div class="module-title">
          <span>未来天气情况</span>
        </div>
        <RightCenter v-if="showCharts" :forecast_24h="forecast_24h"/>
        <span class="line line-top"></span>
        <span class="line line-right"></span>
        <span class="line line-bottom"></span>
        <span class="line line-left"></span>
      </div>
      <div class="module right-bottom">
        <div class="module-title">
          <span>历史气候</span>
        </div>
        <RightBottom v-if="showCharts"/>
        <span class="line line-top"></span>
        <span class="line line-right"></span>
        <span class="line line-bottom"></span>
        <span class="line line-left"></span>
      </div>
    </div>
  </div>
</template>
  
<script setup lang='ts'>
import { ref } from 'vue'
import LeftTop from './components/LeftTop.vue'
import LeftCenter from './components/LeftCenter.vue'
import LeftBottom from './components/LeftBottom.vue'
import RightTop from './components/RightTop.vue'
import RightCenter from './components/RightCenter.vue'
import RightBottom from './components/RightBottom.vue'
import Center from './components/Center.vue'
let observe:any = {}
let indexTips:any = {}
let forecast_24h:any = {}
let air:any = {}
let tips:any = ''
let alarm = {}
let showCharts:any = ref(false)

let obj = {
  url: 'https://wis.qq.com/weather/common',
  data:{
      source:'pc',
      weather_type:'observe|forecast_1h|forecast_24h|index|alarm|limit|tips|rise|air',
      province:"山东省",
      city:"枣庄市",
      county: '滕州市'
  },
  success:(res: any) => {
    console.log(res)
    if (res.status == 200) {
      air = res.data.air
      observe = res.data.observe
      indexTips = res.data.index
      forecast_24h = res.data.forecast_24h
      tips = res.data.tips.observe[0]
      alarm = res.data.alarm
      showCharts.value = true
    }
  }
}
myjsonp(obj)
console.log(showCharts)


function myjsonp(options: any){
  const {data} = options
  let script = document.createElement("script");
  let urlparam = '';
  for(let key in data){
      urlparam = urlparam+key+'='+data[key]+"&"
  }
  let fn: any = 'jsonp'+Math.random().toString().substr(3,10)
  window[fn] = options.success
  script.src = options.url+"?"+urlparam+'callback='+fn;
  document.body.appendChild(script)
  script.onload = function(){
      document.body.removeChild(script)
  }
}
</script>
  
<style lang="less" scoped>
.home {
  display: flex;
  background: #080a34;
  height: calc(100vh - 75px);
  box-sizing: border-box;
  padding: 10px;
  position: relative;
  margin-top: 75px;
  .top {
    position: absolute;
    top: -75px;
    left: 0;
    width: 100vw;
    height: 75px;
    line-height: 75px;
    background: linear-gradient(to right,#080a34 0%, #112259 50%, #080a34 100%);
    // text-align: center;
    img {
      height: inherit;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
    .top-title {
      text-align: center;
      font-size: 30px;
      font-weight: bold;
      background: -webkit-linear-gradient(#02b5ff, #64eef8);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }
  }
  .left {
    flex: 1;
    height: 100%;
    display: flex;
    flex-direction: column;
    .left-top {
      // flex: 1;
    }
    .left-center {
      flex: 1;
      margin-top: 20px;
    }
    .left-bottom {
      flex: 1;
      margin-top: 20px;
    }
  }
  .center {
    flex: 2;
  }
  .right {
    flex: 1;
    height: 100%;
    display: flex;
    flex-direction: column;
    .module .module-title {
      height: 30px;
      line-height: 30px;
    }
    .right-top {
      flex: 1;
    }
    .right-center {
      flex: 1;
      margin-top: 20px;
    }
    .right-bottom {
      flex: 1;
      margin-top: 20px;
    }
  }
}
.module {
  background: #080a34;
  padding: 0 15px 15px;
  box-shadow: rgb(29, 72, 196) 0px 0px 6px 0px inset;
  position: relative;
  overflow: hidden;
  .module-title {
    margin-top: 1px;
    height: 40px;
    line-height: 40px;
    font-weight: bold;
    color: #fff;
    text-align: center;
    background: linear-gradient(to right, #080a34 0%, #113574 50%, #080a34 100%);
  }
  .line {
    position: absolute;
    &.line-top {
      top: 0;
      left: 0;
      width: 100%;
      height: 3px;
      background: linear-gradient(90deg, transparent, #5ba6ff);
      animation: move1 8s linear infinite;
    }
    &.line-right {
      top: -100%;
      right: 0;
      width: 3px;
      height: 100%;
      background: linear-gradient(180deg, transparent, #5ba6ff);
      animation: move2 8s linear infinite;
      animation-delay: 2s;
    }
    &.line-bottom {
      bottom: 0;
      right: -100%;
      width: 100%;
      height: 3px;
      background: linear-gradient(270deg, transparent, #5ba6ff);
      animation: move3 8s linear infinite;
      animation-delay: 4s;
    }
    &.line-left {
      bottom: -100%;
      left: 0;
      width: 3px;
      height: 100%;
      background: linear-gradient(360deg, transparent, #5ba6ff);
      animation: move4 8s linear infinite;
      animation-delay: 6s;
    }
  }
}
@keyframes move1 {
  0% {
    left: -100%;
  }
  50%, 100% {
    left: 100%;
  }
}
@keyframes move2 {
  0% {
    top: -100%;
  }
  50%, 100% {
    top: 100%;
  }
}
@keyframes move3 {
  0% {
    right: -100%;
  }
  50%, 100% {
    right: 100%;
  }
}
@keyframes move4 {
  0% {
    bottom: -100%;
  }
  50%, 100% {
    bottom: 100%;
  }
}
</style>