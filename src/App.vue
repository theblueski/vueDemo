<template>
  <div id="app">
    <div class="left-area">
      <div class="pic-area">
          <div class="top-dot-area">
            <div class="dot">
              <div class="line"></div>
            </div>
            <div class="dot">
              <div class="line"></div>
            </div>
          </div>
      </div>
      <div class="content-area">
          <div class="bottom-dot-area">
            <div class="dot"></div>
            <div class="dot"></div>
          </div>
      </div>
    </div>
<!--    <div style="width: 100%;height: 100%;">-->
<!--      <LinesChart-->
<!--          unit="元"-->
<!--          :colors="['red', 'yellow']"-->
<!--          :data="lineData"/>-->
<!--    </div>-->
<!--    <div class="infoWrapper">-->
<!--      <DashBoard unit="个" :data="40"/>-->
<!--    </div>-->
<!--    <div style="width: 600px;height: 600px;background: #000;">-->
<!--&lt;!&ndash;      <BarsChart :vertical="true" unit="元" :colors="['red', 'pink']" :data="lineData" />&ndash;&gt;-->
<!--      <RadarChart :data="radarData" :indicator="indicator"/>-->
<!--    </div>-->
<!--    <div class="linerLine"></div>-->
<!--    <div class="noover"></div>-->
<!--    <div class="outer ">-->
<!--      <div class="inner">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusantium adipisci dolores, illo magni maiores modi officia quo voluptatem? Autem commodi dolores ducimus esse id magni mollitia quia quidem recusandae sequi.</div>-->
<!--    </div>-->
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import {DashBoard, LinesChart, BarsChart, RadarChart} from './components/charts'
export default {
  name: 'app',
  components: {
    // HelloWorld
    DashBoard,
    LinesChart,
    BarsChart,
    RadarChart
  },
  data() {
    return {
      indicator: [
        { name: 'Sales', max: 100 },
        { name: 'Administration', max: 100 },
        { name: 'Information Technology', max: 100 },
        { name: 'Customer Support', max: 100 },
        { name: 'Development', max: 100 },
        { name: 'Marketing', max: 100 }
      ],
      radarData1: {
        'ser1': [80, 90, 70,60,80, 96],
        'ser2': [60, 40, 80, 40, 50, 30]
      },
      radarData: [
        {
          name: 'ser1',
          value: [80, 90, 70,60,80, 96]
        },
        {
          name: 'ser2',
          value: [60, 40, 80, 40, 50, 30]
        }
      ],
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
  width: 100%;
  height: 100vh;
  background: #333;
  position: relative;
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
<style lang="less">
.left-area {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  background: pink;
  width: 400px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  .pic-area {
    position: relative;
    flex-shrink: 0;
    width: 100%;
    height: 400px;
    margin-bottom: 16px;
    background: yellow;
    .top-dot-area {
      z-index: 100;
      position: absolute;
      width: 200px;
      transform: translateX(-50%);
      left: 50%;
      display: flex;
      align-items: center;
      justify-content: space-between;
      bottom: 20px;
      .dot {
        position: relative;
        .line {
          position: absolute;
          width: 2px;
          height: 65px;
          background: violet;
          top: 42px;
          left: 50%;
          transform: translateX(-50%);
          &::after {
            content: '';
            width: 0;
            height: 0;
            border: 6px solid transparent;
            position: absolute;
            bottom: -8px;
            left: 50%;
            transform: translateX(-50%);
            border-top-color: red;
          }
        }
      }
    }
  }
  .content-area {
    position: relative;
    width: 100%;
    height: 100%;
    background: blue;
    .bottom-dot-area {
      position: absolute;
      width: 200px;
      top: 40px;
      transform: translateX(-50%);
      left: 50%;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
  }
  .dot {
    width: 40px;
    height: 40px;
    border-radius: 40px;
    background: #333;
  }
}
</style>
