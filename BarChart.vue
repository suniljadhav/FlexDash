<template>
  <div>
    <canvas ref="barChartCanvas"></canvas>
  </div>
</template>

<script>

export default {
  name: "BarChart",

  props: {
    data: {
      type: Array,
      default: () => [],
      validator(v) {
        // Add validation logic if needed
        return Array.isArray(v);
      },
      tip: "Array of data points for the bar chart",
    },
    labels: {
      type: Array,
      default: () => [],
      tip: "Array of labels for the bar chart",
    },
    colors: {
      type: Array,
      default: () => [],
      tip: "Array of colors for the bar chart, names or #rrggbb",
    },
    // Additional customization options for the bar chart
    barChartOptions: {
      type: Object,
      default: () => ({}),
      tip: "Additional customization options for the bar chart (Chart.js options)",
    },
  },

  mounted() {
    this.renderBarChart();
  },

  methods: {
    renderBarChart() {
      const ctx = this.$refs.barChartCanvas.getContext('2d');

      const barChartData = {
        labels: this.labels,
        datasets: [{
          label: 'Bar Chart Data',
          backgroundColor: this.colors,
          data: this.data,
        }],
      };

      // Merge additional customization options with default options
      const mergedOptions = Object.assign(
        {
          responsive: true,
          maintainAspectRatio: false,
          scales: {
            x: {
              type: 'category', // Specify the x-axis type as category if needed
            },
            y: {
              beginAtZero: true, // Customize y-axis options as needed
            },
          },
        },
        this.barChartOptions // Customization options provided through props
      );

      // Create the bar chart using Chart.js with merged options
      new Chart(ctx, {
        type: 'bar',
        data: barChartData,
        options: mergedOptions,
      });
    },
  },
};
</script>

<style scoped>
/* Add scoped CSS styles if needed */
</style>