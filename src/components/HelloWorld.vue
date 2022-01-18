<template>
  <div class="wrapper">
    <FlowCHart />
  </div>
</template>

<script>
import FlowChart from './flowChart'
export default {
  name: 'HelloWorld',
  components: {
    FlowChart
  },
  props: {
    msg: String
  },
  mounted() {
    this.init()
    this.draw()
  },
  methods: {

  },
  data() {
    return  {

    }
  }
}
</script>

<style scoped>
  .wrapper {
    width: 100%;
    height: 100%;
    padding: 60px;
  }
</style>
