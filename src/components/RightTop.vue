<template>
  <div ref="chart" class="chart"></div>
</template>

<script setup lang="ts">
import { ref, onMounted, defineProps } from 'vue'
import * as echarts from 'echarts';
const props = defineProps({
  forecast_24h: Object
})
const chart = ref(null)
onMounted(() => {
  let xAxisData = []
  let minData = []
  let maxData = []
  for(let item in props.forecast_24h) {
    const dataArr = props.forecast_24h[item].time.split('-')
    xAxisData.push(dataArr[1]+dataArr[2])
    minData.push(props.forecast_24h[item].min_degree)
    maxData.push(props.forecast_24h[item].max_degree)
  }
  const myChart = echarts.init(chart.value, 'dark');
  myChart.setOption({
    backgroundColor: '#080a34',
    grid: {
      top: 20,
      bottom: 20,
    },
    legend: {
      show: false,
      data: ['最高气温', '最低气温']
    },
    tooltip: {
      trigger: 'axis'
    },
    xAxis: {
      type: 'category',
      boundaryGap: false,
      data: xAxisData
    },
    yAxis: {
      type: 'value'
    },
    series: [
      {
        name: '最高气温',
        type: 'line',
        data: maxData
      },
      {
        name: '最低气温',
        type: 'line',
        data: minData
      },
    ]
  });
})
</script>

<style lang="less" scoped>
.chart {
  height: calc(100% - 30px);
}
</style>