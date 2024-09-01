<template>
  <div class="box">
    <div class="line">{{ indexTips?.carwash?.detail }}</div>
    <div class="line">{{ indexTips?.clothes?.detail }}</div>
    <div class="line">{{ indexTips?.fish?.detail }}</div>
    <div class="line">{{ indexTips?.sports?.detail }}</div>
    <div class="line">{{ indexTips?.sunscreen?.detail }}</div>
    <div class="line">{{ indexTips?.umbrella?.detail }}</div>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue';
const props = defineProps({
  indexTips: Object,
})

</script>

<style lang="less" scoped>
.box {
  height: calc(100% - 30px);
  overflow: hidden;
  overflow-y: auto;
}
.line {
  padding: 10px 20px;
  color: #fff;
  &:nth-child(odd) {
    background: #080a34;
  }
  &:nth-child(even) {
    background: #113473;
  }
}
/* 自定义整个滚动条 */
::-webkit-scrollbar {
  width: 0px; /* 滚动条宽度 */
}
 
/* 自定义滚动条轨道 */
::-webkit-scrollbar-track {
  background: #f1f1f1; /* 轨道颜色 */
}
 
/* 自定义滚动条的滑块（thumb） */
::-webkit-scrollbar-thumb {
  background: #888; /* 滑块颜色 */
}
 
/* 当滑块悬停或活动时的样式 */
::-webkit-scrollbar-thumb:hover {
  background: #555; /* 滑块悬停颜色 */
}
</style>