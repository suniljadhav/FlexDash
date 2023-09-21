<template>
  <div>
    <canvas ref="chart"></canvas>
  </div>
</template>

<script>
import Chart from 'chart.js';

export default {
  props: ['data'],
  mounted() {
    this.renderChart();
  },
  methods: {
    renderChart() {
      const ctx = this.$refs.chart.getContext('2d');
      new Chart(ctx, {
        type: 'bar',
        data: {
          labels: this.data.labels,
          datasets: [
            {
              label: 'Bar Chart Data',
              data: this.data.values,
              backgroundColor: 'rgba(75, 192, 192, 0.2)',
              borderColor: 'rgba(75, 192, 192, 1)',
              borderWidth: 1,
            },
          ],
        },
      });
    },
  },
};
</script>

<style scoped>
/* Add CSS styles here */
</style>