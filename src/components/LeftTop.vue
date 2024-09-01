<template>
  <div>
    <div class="top">
      <div class="num">{{observe?.degree}}°</div>
      <div class="weather">{{ observe?.weather }}</div>
      <!-- <div class="aqi">28 优</div> -->
    </div>
    <div class="center">
      <div class="box">
        <img src="../assets/weather/wind.png" />
        <span>{{ observe?.wind_direction_name }} {{ observe?.wind_power }}级</span>
      </div>
      <div class="box">
        <img src="../assets/weather/humidity.png" />
        <span>湿度 {{ observe?.humidity }}%</span>
      </div>
      <div class="box">
        <img src="../assets/weather/air.png" />
        <span>气压 {{ observe?.pressure }}hPa</span>
      </div>
    </div>
    <div class="tips">● {{ tips }}</div>
  </div>
</template>
  
<script setup lang='ts'>
import { defineProps } from 'vue';
const props = defineProps({
  observe: Object,
  tips: String
})
console.log(12345679)
</script>
  
<style lang="less" scoped>
.top {
  display: flex;
  align-items: baseline;
  color: #fff;
  .num {
    font-size: 50px;
  }
  .weather {
    flex: 1;
    margin-left: 10px;
    font-size: 20px;
  }
  .aqi {
    background: #a3d765;
    border-radius: 10px;
    padding: 2px 8px;
  }
}
.center {
  display: flex;
  margin-top: 10px;
  .box {
    display: flex;
    align-items: center;
    font-size: 14px;
    color: #fff;
    &:not(:last-child) {
      margin-right: 30px;
    }
    img {
      width: 16px;
      height: 16px;
    }
    span {
      margin-left: 10px;
    }
  }
}
.tips {
  font-size: 14px;
  margin-top: 20px;
  color: #fff;
}
</style>