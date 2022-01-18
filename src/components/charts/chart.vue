<template>
  <div ref="chartRef" class="chartWrapper"></div>
</template>
<script>
import * as echarts from 'echarts'

function throttle(fn, ms = 50) {
  let handler = null
  return (...args) => {
    if(window.requestAnimationFrame) {
      window.requestAnimationFrame(() => {fn(...args)})
    } else {
      if(handler) return
      handler = setTimeout(() =>{
        fn(...args)
        handler = null
      }, ms)
    }
  }
}

export default {
  name: 'chart',
  props: {
    option: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      chart: null,
      resizeHandler: null
    }
  },
  mounted() {
    this.chart = echarts.init(this.$refs.chartRef)
    this.addResizeHandler()
    if(this.option) {
      this.setChart(this.option)
    }
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.resizeHandler)
  },
  methods: {
    addResizeHandler() {
      this.resizeHandler = throttle(() => {
        this.chart.resize()
      })
      window.addEventListener('resize', this.resizeHandler)
    },
    setChart(option) {
      this.chart.setOption(option)
    }
  },
  watch: {
    option(val) {
      if(val) {
        this.setChart(val)
      }
    }
  }
}
</script>
<style scoped>
  .chartWrapper {
    width: 100%;
    height: 100%;
  }
</style>
