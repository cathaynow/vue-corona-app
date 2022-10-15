<template>
  <canvas ref="myChart" width="500" height="500"></canvas>
</template>

<script>
import { Chart, registerables } from "chart.js";
Chart.register(...registerables);
export default {
  name: "ChartGraph",
  props: {
    chartOptions: {
      type: Object,
      default() {
        return {
          type: "bar",
          labels: ["Red", "Blue"],
          datasets: [
            {
              data: [12, 19],
              label: "테스트",
              borderWidth: 1,
              backgroundColor: ["rgba(255,99,132,0.2)", "rgba(54,162,235,0.2)"],
              borderColor: ["rgba(255,99,132,1)", "rgba(54,162,235,1)"],
            },
          ],
          options: {
            scales: {
              y: {
                beginAtZero: true,
              },
            },
          },
        };
      },
    },
  },
  data() {
    return {
      chartObject: null,
    };
  },
  mounted() {
    this.drawChart();
  },
  methods: {
    drawChart() {
      const { type, datasets, labels, options } = this.chartOptions;
      const ctx = this.$refs.myChart.getContext("2d");
      this.chartObject = new Chart(ctx, {
        type: type,
        data: {
          labels,
          datasets,
        },
        options,
      });
    },
  },
};
</script>

<style></style>
