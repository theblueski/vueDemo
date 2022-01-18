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
    data: {
      type: Array,
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
      default: 20
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
      this.option = {
        series: [
          {
            type: 'gauge',
            startAngle: 225,
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
            data
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
