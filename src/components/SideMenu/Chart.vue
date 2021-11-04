<template>
  <Pie ref="chart" />
</template>

<script>
import { Pie } from "vue-chartjs";

export default {
  name: "Chart",
  props: {
    data: {
      type: Array,
      required: true,
    },
  },
  components: {
    Pie,
  },

  data: () => ({
    chartData: null,
    options: null,
  }),

  mounted() {
    this.makeChart();
  },
  methods: {
    makeChart() {
      this.chartData = {
        labels: this.data.map((legendItem) => legendItem.text),
        datasets: [
          {
            label: "Легенда",
            backgroundColor: this.data.map((legendItem) => legendItem.color),
            data: this.data.map((legendItem) => legendItem.counter),
          },
        ],
      };
      this.options = {
        legend: {
          display: false,
        },
      };

      this.$refs.chart.renderChart(this.chartData, this.options);
    },
  },
};
</script>

<style scoped></style>
