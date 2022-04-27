<template>
  <div class="container">
    <BarChart v-if="loaded" :chartData="chartData" />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import BarChart from '@/components/BarChart.vue'

export default Vue.extend({
  name: 'IndexPage',

  data: () => ({
    loaded: false,
  }),

  async asyncData({ $axios }) {
    const result = await $axios.$get('/api/result', {
      params: {
        studentID: 304,
      },
    })

    const chartData = {
      labels: result.results.map((res) => res.examID),
      datasets: [
        {
          label: 'Student',
          data: result.results.map((res) => res.result),
        },
        {
          label: 'Average',
          data: result.results.map((res) => res.avg),
        },
      ],
    }

    return { chartData, loaded: true }
  },

  components: { BarChart },
})
</script>
