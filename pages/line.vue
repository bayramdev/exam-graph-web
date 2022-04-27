<template>
  <section>
    <h1>Hello to line chart!</h1>
    <LineChart
      v-if="loaded"
      :chartData="chartData"
      :chartOptions="chartOptions"
    />
  </section>
</template>

<script lang="ts">
import Vue from 'vue'
import { Line as LineChart } from 'vue-chartjs/legacy'

import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  CategoryScale,
  LinearScale,
  PointElement,
} from 'chart.js'

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement
)

export default Vue.extend({
  components: { LineChart },

  data: () => ({
    chartData: {},
    chartOptions: {
      responsive: true,
      scales: {
        y: {
          beginAtZero: true,
          title: {
            display: true,
            text: 'Marks',
          },
        },
        x: {
          title: {
            display: true,
            text: 'Exams',
          },
        },
      },
    },
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
          borderColor: '#0000ff',
          backgroundColor: '#0000ff88',
        },
        {
          label: 'Average',
          data: result.results.map((res) => res.avg),
          borderColor: '#ff0000',
          backgroundColor: '#ff000088',
        },
      ],
    }

    return { chartData, loaded: true }
  },
})
</script>
