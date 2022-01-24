<template>
  <Chart :option="option"/>
</template>
<script>
import Chart from '../chart'
export default {
  name: 'dashBoard',
  components: {
    Chart
  },
  props: {
    // 设置进度条最大值
    unit: {
      type: String,
      default: ''
    },
    max: {
      type: Number,
      default: 100
    },
    // 直接输入进度
    data: {
      type: Number,
      required: true
    },
    background: {
      type: String,
      default: 'green'
    }, // 圆环背景色
    foreground: {
      type: String,
      default: 'red'
    },   // 进度条颜色
    width: {
      type: Number,
      default: 10
    },  // 圆环的宽度
  },
  mounted() {
    this.setOption(this.data)
  },
  data() {
    return {
      option: {
      }
    }
  },
  methods: {
    setOption(data) {
      const _this = this
      this.option = {
        series: [
          {
            type: 'gauge',
            startAngle: 225,
            radius: '100%',
            min: 0,
            max: this.max,
            endAngle: -45,
            pointer: {
              show: false,
            },
            progress: {
              show: true,
              roundCap: true,
              clip: false,
              overlap: false,
              itemStyle: {
                color: this.foreground,
              }
            },
            axisLine: {
              roundCap: true,
              lineStyle: {
                width: this.width,
                // color: this.background
              }
            },
            splitLine:  {
              show: false
            },
            axisTick: {
              show: false
            },
            axisLabel: {
              show: false
            },
            title: {
              show: false
            },
            data: [{
              value: data
            }],
            detail: {
              offsetCenter: [0, 0],
              formatter(val) {
                const unit = _this.unit
                const arr = [
                  `{a|${val}}`,
                  `{b|${unit}}`,
                ];
                return arr.join('');
              },
              rich: {
                'a': {
                  color: 'red',
                  fontSize: 30,
                  fontWeight: 'bold',
                  padding: [0, 4, 0, 0]
                },
                'b': {
                  color: '#fff',
                  fontSize: 12,
                  padding: [10, 0, 0, 0]
                }
              }
            },
          }
        ]
      }
    }
  },
  watch: {
    data(val) {
      if(val) {
        this.setOption(val)
      }
    }
  }
}
</script>
<style></style>
