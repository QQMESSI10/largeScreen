<template>
  <div class="center">
    <div class="top-tips">
      <div v-for="(item, index) in alarm">
        <template v-if="index == '0'">{{ item.detail }}</template>
      </div>
    </div>
    <div ref="chart" class="chart"></div>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted, defineProps } from 'vue'
import * as echarts from 'echarts';
import tzMap from '../map/tz.json'
const props = defineProps({
  alarm: Object,
})
const chart = ref(null)
onMounted(() => {
  const tzJson: any = tzMap
  const myChart = echarts.init(chart.value, 'dark');
  console.log('tzMap')
  console.log(tzMap)
  echarts.registerMap('ZZ', tzJson);
  var option = {
    backgroundColor: '#080a34',
    tooltip: {
      formatter: '{b0}: {c0}°'
    },
    series: [
      {
        name: '枣庄地图',
        type: 'map',
        map: 'ZZ',// 这个是上面注册时的名字哦，registerMap（'这个名字保持一致'）
        label: {
          show: true,
        },
        data: [
          { name: '滕州市', itemStyle: { areaColor: '#a3d765' }, value: '20' },
          { name: '山亭区', value: '10' },
          { name: '薛城区', value: '10' },
          { name: '市中区', value: '10' },
          { name: '峄城区', value: '10' },
          { name: '台儿庄区', value: '10' },
        ]
      }
    ]
  };
  myChart.setOption(option)
})
</script>

<style lang="less" scoped>
.center {
  position: relative;
  height: calc(100% - 30px);
  overflow: hidden;
  .chart {
    width: 100%;
    height: 100%;
    padding-top: 50px;
  }
  .top-tips {
    position: absolute;
    left: 20px;
    top: 20px;
    color: #fddd60;
    z-index: 99;
  }
}
</style>