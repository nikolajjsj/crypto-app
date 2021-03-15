<template>
  <canvas id="myChart"></canvas>
</template>

<script>
import Chart from 'chart.js'

export default {
  name: 'CryptoChart',
  props: {
    cryptoData: {
      type: Array,
      required: true
    },
    labels: {
      type: Array,
      required: true
    }
  },
  mounted () {
    var myChart = new Chart(document.getElementById('myChart'), {
      type: 'line',
      data: {
        labels: this.labels,
        datasets: [
          {
            label: 'Prices last 7 days',
            data: this.cryptoData,
            backgroundColor: '#2c3e50'
          }
        ]
      }
    })
    console.log(myChart)
  }
}
</script>

<style>
#myChart {
  height: 200px;
  width: 200px;
}
</style>
