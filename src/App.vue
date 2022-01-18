<template>
  <div id="app">
<!--    <DashBoard :data="dashBoardData"/>-->
    <BarsChart  :data="lineData" />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import { DashBoard, LinesChart, BarsChart } from './components/charts'
export default {
  name: 'app',
  components: {
    // HelloWorld
    DashBoard,
    LinesChart,
    BarsChart
  },
  data() {
    return {
      option: {
        title: {
          text: 'Echarts 入门示例'
        },
        xAxis: {},
        yAxis: {},
        series: [{
          name: '销量',
          type: 'bar',
          data: [5, 20, 36, 10, 10, 20]
        }]
      },
      dashBoardData: [
      {
        value: 50,
        name: 'SCORE'
      }
    ],
      barData: [{
        name: '1月',
        value: 1000
      },
        {
          name: '2月',
          value: 100
        },
        {
          name: '3月',
          value: 200
        },
        {
          name: '4月',
          value: 3000
        },{
          name: '5月',
          value: 20
        },{
          name: '6月',
          value: 121
        }],
      lineData: {
        '我的': [{
          name: '1月',
          value: 1000
        },
          {
            name: '2月',
            value: 100
          },
          {
            name: '3月',
            value: 200
          },
          {
            name: '4月',
            value: 3000
          },{
            name: '5月',
            value: 20
          },{
            name: '6月',
            value: 121
          }],
        '你的': [{
          name: '1月',
          value: 100
        },
          {
            name: '2月',
            value: 1600
          },
          {
            name: '3月',
            value: 800
          },
          {
            name: '4月',
            value: 30
          },{
            name: '5月',
            value: 200
          },{
            name: '6月',
            value: 1210
          }]
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 60%;
  height: 300px;
}
</style>
