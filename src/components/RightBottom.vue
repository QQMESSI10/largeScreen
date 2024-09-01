<template>
  <div ref="chart" class="chart"></div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import * as echarts from 'echarts';
const chart = ref(null)
onMounted(() => {
  const myChart = echarts.init(chart.value, 'dark');
  myChart.setOption({
    backgroundColor: '#080a34',
    grid: {
      top: 40,
      left: 40,
      right: 60,
      bottom: 20,
    },
    tooltip: {
    trigger: 'axis',
    axisPointer: {
      type: 'cross',
      crossStyle: {
        color: '#999'
      }
    }
  },
  xAxis: [
    {
      type: 'category',
      data: ['1月', '2月', '3月', '4月', '5月', '6月', '7月', '8月', '9月', '10月', '11月', '12月'],
      axisPointer: {
        // type: 'shadow'
      }
    }
  ],
  yAxis: [
    {
      type: 'value',
      name: '温度',
      min: -10,
      max: 35,
      interval: 5,
      axisLabel: {
        formatter: '{value} °C'
      }
    },
    {
      type: 'value',
      name: '降水量',
      min: 0,
      max: 250,
      interval: 50,
      axisLabel: {
        formatter: '{value} mm'
      }
    },
  ],
  series: [
    {
      name: '降水量',
      type: 'bar',
      yAxisIndex: 1,
      tooltip: {
        valueFormatter: function (value: any) {
          return value + ' mm';
        }
      },
      data: [
        10.4, 14.8, 21.4, 31.5, 59.7, 86.6, 162.8, 177.1, 66.2, 33.3, 21.1, 10.1
      ]
    },
    {
      name: '最高气温',
      type: 'line',
      tooltip: {
        valueFormatter: function (value: any) {
          return value + ' °C';
        }
      },
      data: [5.1, 8.3, 13.9, 20.9, 26.3, 30.9, 31.4, 30.6, 27.2, 21.7, 13.8, 7]
    },
    {
      name: '最低气温',
      type: 'line',
      tooltip: {
        valueFormatter: function (value: any) {
          return value + ' °C';
        }
      },
      data: [-4.3, -1.7, 3.2, 9.7, 15.2, 20.4, 23.4, 22.3, 17.2, 10.9, 3.5, -2.5]
    }
  ]
  });
})
</script>

<style lang="less" scoped>
.chart {
  height: calc(100% - 30px);
}
</style>