<template>
  <div ref="chart" class="chart"></div>
</template>

<script lang="ts" setup>
import { ref, onMounted, defineProps } from 'vue'
import * as echarts from 'echarts';
const chart = ref(null)
const props = defineProps({
  air: Object
})
onMounted(() => {
  const myChart = echarts.init(chart.value);
  myChart.setOption({
    series: [
      {
        type: 'gauge',
        startAngle: 180,
        endAngle: 0,
        center: ['50%', '85%'],
        radius: '90%',
        min: 0,
        max: 500,
        splitNumber: 20,
        axisLine: {
          lineStyle: {
            width: 15,
            color: [
              [0.1, '#25e328'],
              [0.2, '#fffe38'],
              [0.3, '#fc7923'],
              [0.4, '#fc0d1c'],
              [0.6, '#8f0645'],
              [1, '#68021f'],
            ]
          }
        },
        pointer: {
          icon: 'path://M12.8,0.7l12,40.1H0.7L12.8,0.7z',
          length: '30%',
          width: 10,
          offsetCenter: [0, '-60%'],
          itemStyle: {
            color: 'auto'
          }
        },
        axisTick: {
          show: false,
          length: 1,
          lineStyle: {
            color: 'auto',
            width: 2
          },
          itemStyle: {
            color: 'auto'
          }
        },
        splitLine: {
          show: false,
        },
        axisLabel: {
          color: '#fff',
          fontSize: 15,
          distance: -40,
          rotate: 'tangential',
          show: true,
          formatter: function (value: any) {
            if (value === 400) {
              return '严重';
            } else if (value === 250) {
              return '重度';
            } else if (value === 175) {
              return '中度';
            } else if (value === 125) {
              return '轻度';
            } else if (value === 75) {
              return '良';
            } else if (value === 25) {
              return '优';
            }
            return '';
          }
        },
        title: {
          offsetCenter: [0, '-10%'],
          fontSize: 22,
          color: 'inherit'
        },
        detail: {
          fontSize: 15,
          offsetCenter: [0, '-35%'],
          valueAnimation: true,
          color: 'inherit'
        },
        data: [
          {
            value: props.air?.aqi,
            name: props.air?.aqi_name
          }
        ]
      }
    ]
  })
})
</script>

<style lang="less" scoped>
.chart {
  height: calc(100% - 30px);
}
</style>