<template>
  <Chart :option="option"/>
</template>
<script>
import Chart from '../chart'
export default {
  name: 'bars',
  components: {
    Chart
  },
  props: {
    /**
     * 数据格式支持数组，map
     * 分别用于支持单条线和多条线
     * map数据格式类似:
     * {
     *   key: [value1, value2,value3]
     * }
     * key为系列名字
     * value 要求格式：
     * {
     *   name: ${name},
     *   value: ${value}
     * }
     */
    data: {
      required: true
    },
    vertical: {
      type: Boolean,
      default: true
    },
    width: {
      type: Number,
      default: 20
    },  // 圆环的宽度
    // 柱颜色列表
    colors: {
      type: Array,
      default() {
        return []
      }
    }
  },
  mounted() {
    this.option = this.getOptions(this.data)
  },
  data() {
    return {
      option: {
      }
    }
  },
  methods: {
    getIntervals(data) {
      if(!data) return null
      if(data instanceof Array) {
        return data.map(i => i.name)
      }
      if( data instanceof Object) {
        const key = Object.keys(data)[0]
        return data[key].map(i => i.name)
      }
    },
    getValueMap(data) {
      if(!data) return null
      if(data instanceof Array) {
        return data.map(i => i.value)
      }
      if(data instanceof Object) {
        const valueMap = {}
        Object.keys(data).forEach( i => {
          valueMap[i] = data[i].map(val => val.value)
        })
        return valueMap
      }
    },
    getSeries(data) {
      const valueMap = this.getValueMap(data)
      if(!valueMap) return null
      if(valueMap instanceof  Array) {
        return [{
          data: valueMap,
          type: 'bar',
          barMaxWidth: this.width,
          barGap: 0,
          itemStyle: {
            color: this.colors[0]
          }
        }]
      }
      if(valueMap instanceof  Object) {
        return Object.keys(valueMap).map((i,index) => ({
          data: valueMap[i],
          name: i,
          type: 'bar',
          barMaxWidth: this.width,
          barGap: 0,
          itemStyle: {
            color: this.colors[index]
          }
        }))
      }
    },
    getOptions(data) {
      const intervals = this.getIntervals(data)
      const series = this.getSeries(data)
      if(!intervals || !series) {
        // console.log('线图：数据结构不正常，或者数据为空')
        return {}
      }

      const yAxis = this.vertical ? {
        type: 'value',
        splitLine: {
          show: false
        },
        axisTick: {
          show: false
        },
        axisLabel: {
          show: false
        }
      } : {
        type: 'category',
        data: intervals,
        axisTick: {
          show: false,
        },
        axisLine: {
          lineStyle: {
            color: '3ccc',
          },
        },
      }

      const xAxis = this.vertical ? {
        type: 'category',
        data: intervals,
        axisLabel: {
          color: '#000',
          rotate: 35,
          margin: 15,
          interval: 0, //横轴信息全部显示
        },
        axisTick: {
          show: false,
        },
        axisLine: {
          lineStyle: {
            color: '3ccc',
          },
        },
      } : {
        type: 'value',
        splitLine: {
          show: false
        },
        axisTick: {
          show: false
        },
        axisLabel: {
          show: false
        }
      }
      return {
        tooltip: {
          trigger: 'axis',
        },
        legend: {
          icon: 'roundRect',
          itemHeight: 10,
          itemGap: 20,
          top: 20,
          right: 20
          // align: 'auto' // 控制图标和icon位置
        },
        grid: {
          top: '16%',
          left: '5%',
          right: '6%',
          bottom: '2%',
          containLabel: true,
        },
        xAxis,
        yAxis,
        series
      }
    }
  },
  watch: {
    data(val) {
      if(val) {
        this.option = this.getOptions(val)
      }
    }
  }
}
</script>
<style></style>
