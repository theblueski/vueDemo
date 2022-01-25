<template>
  <Chart :option="option"/>
</template>
<script>
import Chart from '../chart'
export default {
  name: 'lines',
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
    width: {
      type: Number,
      default: 20
    },  // 圆环的宽度
    unit: {
      type: String,
      default: ''
    },
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
          type: 'line',
          symbolSize: 6,
          symbol: 'circle',
          lineStyle: {
            width: 1,
            color: this.colors[0]
          },
          itemStyle: {
            color: this.colors[0]
          }
        }]
      }
      if(valueMap instanceof  Object) {
        return Object.keys(valueMap).map((i,index) => ({
          data: valueMap[i],
          type: 'line',
          symbolSize: 6,
          symbol: 'circle',
          lineStyle: {
            width: 1,
            color: this.colors[index]
          },
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
      return {
        legend: {
          icon: 'circle',
          itemHeight: 10,
          itemGap: 20,
          top: 20,
        },
        grid: {
          top: '20%',
          left: '4%',
          right: '2%',
          bottom: '2%',
          containLabel: true,
        },
        xAxis: {
          type: 'category',
          data: intervals,
          axisLabel: {
            color: '#000',
            rotate: 45,
            margin: 15,
          },
          axisTick: {
            show: false,
          },
          axisLine: {
            lineStyle: {
              color: '#e8ecef',
            },
          },
        },
        yAxis: {
          type: 'value',
          splitLine: {
            show: false
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            show: false
          },
          name: this.unit,
          nameTextStyle: {
            color: '#fff'
          },
          offset: -10,
          nameGap: 8, // 名字位置
          axisLine: {
            show: true,
            lineStyle: {
              color: '#e8ecef',
            },
          },
        },
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
