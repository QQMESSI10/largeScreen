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
  let seriesData:any = []
  for(let item in props.forecast_24h) {
    const name = props.forecast_24h[item].day_weather
    const obj = seriesData.find((f: any) => f.name == name)
    if (obj) {
      obj.value++
    } else {
      seriesData.push({value: 1,name})
    }
  }
  const myChart = echarts.init(chart.value, 'dark');
  myChart.setOption({
    backgroundColor: '#080a34',
    grid: {
      top: 0,
      bottom: 0,
    },
    tooltip: {
      trigger: 'item',
      formatter: '{b0}{c0}天'
    },
    series: [
      {
        name: 'Radius Mode',
        type: 'pie',
        radius: '80%',
        emphasis: {
          label: {
            show: true
          }
        },
        data: seriesData
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