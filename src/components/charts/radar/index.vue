<template>
  <Chart :option="option"/>
</template>
<script>
import Chart from '../chart.vue'

const colorStops = [0.1,0.2,0.4,0.6,0.8,1]

const lineStyle = {
  width: 1,
  opacity: 0.5
};

export default {
  name: 'radar',
  props: {
    /**
     * 格式
     * {
     *   name: String,
     *   max: Number
     * }
     */
    indicator: {
      type: Array,
      required: true
    },
    /**
     * 支持Array和Object
     * Array格式
     * {
     *   name: String,
     *   value: Array
     * }
     *
     * Object格式
     * {
     *   name: Array
     * }
     *
     * Array为纯数据
     */
    data: {
      required: true
    },
    shape: {
      type: String,
      default: 'polygon'  // 支持 polygon | circle
    },
    bgLineColor: {
      type: String,
      default: 'rgb(255,255,255)'
    },
    axisColor: {
      type: String,
      default: 'rgb(255,255,255)'
    },
    areaColor: {
      type: Array,
      default() {
        return ['red', 'blue']
      }
    }
  },
  components: {
    Chart
  },
  data() {
    return {

    }
  },
  methods: {
    getSeries(data) {
      let handledData = null
      if(data instanceof Array) {
        handledData = data.map((i,index) => ({
          ...i,
          lineStyle: {
            color: this.areaColor[index],
            opacity: 0.4
          },
          areaStyle: {
            color: this.areaColor[index],
            opacity: 0.4
          }
        }))
      } else {
        handledData = Object.keys(data).map((i,index) => ({
          name: i,
          value: data[i],
          lineStyle: {
            color: this.areaColor[index],
            opacity: 0.4
          },
          areaStyle: {
            color: this.areaColor[index],
            opacity: 0.4
          }
        }))
      }

      return [{
        type: 'radar',
        symbol: 'none',
        lineStyle: lineStyle,
        data:handledData
      }]
    },
    getBgLines(color) {
      const handledColor = color.replace('rgb', 'rgba')
      const index = handledColor.lastIndexOf(')')
      return colorStops.map(i => handledColor.substr(0, index) + `,${i})`).reverse()
    },
    getAxisLineColor(color) {
      const handledColor = color.replace('rgb', 'rgba')
      const index = handledColor.lastIndexOf(')')
      return handledColor.substr(0, index) + `,0.5)`
    }
  },
  computed: {
    option() {
      const series = this.getSeries(this.data)
      return {
        radar: {
          // radius: '75%',
          axisName: {
            show: true,
            color: '#fff',
            overflow: 'truncate'
          },
          splitNumber: 5,
          splitArea: {
            show: false
          },
          shape: this.shape,
          indicator: this.indicator,
          axisLine: {
            lineStyle: {
              color: this.getAxisLineColor(this.axisColor)
            }
          },
          splitLine: {
            lineStyle: {
              color: this.getBgLines(this.bgLineColor)
            }
          },
        },
        series
      }
    }
  }
}
</script>
<style></style>
