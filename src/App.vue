<template>
  <div id="app">
    <div class="infoWrapper">
      <DashBoard unit="个" :data="40"/>
    </div>
<!--    <BarsChart  :data="lineData" />-->
<!--    <div class="linerLine"></div>-->
<!--    <div class="noover"></div>-->
<!--    <div class="outer ">-->
<!--      <div class="inner">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusantium adipisci dolores, illo magni maiores modi officia quo voluptatem? Autem commodi dolores ducimus esse id magni mollitia quia quidem recusandae sequi.</div>-->
<!--    </div>-->
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
        value: 40,
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
.linerLine {
  width: 200px;
  height: 2px;
  background-image: linear-gradient(to right, red, transparent 60%);
}
.outer {
  width: 100px;
  height: 100px;
  overflow-x: hidden;
  overflow-y: auto;
}
.inner {
  width: 100%;
}

/*ie兼容*/
div {
  /*三角箭头颜色*/
  scrollbar-arrow-color: #fff;
  /*滚动条滑块按钮颜色*/
  scrollbar-face-color: #0099dd;
  /*滚动条整体颜色*/
  scrollbar-highlight-color: #0099dd;
  /*滚动条阴影*/
  scrollbar-shadow-color: #0099dd;
  /*滚动条滑轨颜色*/
  scrollbar-track-color: #0066ff;
  /*滚动条3d亮色阴影边框的外观颜色——左边和上边的阴影色*/
  scrollbar-3dlight-color: #0099dd;
  /*滚动条3d暗色阴影边框的外观颜色——右边和下边的阴影色*/
  scrollbar-darkshadow-color: #0099dd;
  /*滚动条基准颜色*/
  scrollbar-base-color: #0099dd;
}


/*chrome & safari 浏览器*/
/*滚动条整体部分,必须要设置*/
div::-webkit-scrollbar {
  width: 2px;
  height: 2px;
  background-color: yellow;
}
/*滚动条的轨道*/
div::-webkit-scrollbar-track {
  background-color: yellow;
}
/*滚动条的滑块按钮*/
div::-webkit-scrollbar-thumb {
  border-radius: 0;
  background-color: green;
  box-shadow: inset 0 0 5px yellow;
}
/*滚动条的上下两端的按钮*/
div::-webkit-scrollbar-button {
  height: 0;
  background-color: #0099ff;
}
.noover {
  width: 100px;
  height: 100px;
  background: pink;
}
.infoWrapper {
  width: 90px;
  height: 90px;
}
</style>
