<template>
  <Chart />
</template>
<script>
import Chart from '../chart.vue'
export default {
  name: 'radar',
  props: {
    data: {
      type
    }
  },
  components: {
    Chart
  }
}
</script>
<style></style>
