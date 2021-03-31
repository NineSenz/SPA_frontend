<template>
  <div class="chartElem">
    <div class="row">
      <highcharts class="chart" :options="chartOptions" :updateArgs="updateArgs"></highcharts>
      <div>
        <h3>Flexibly change the value of each point:</h3>
        <h4>Points:</h4>
        <form class="row points">
          <div v-for="index in 8" :key="index">
            <p>{{index}}</p>
            <input v-model.number="points[index-1]" type="number" class="numberInput">
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      title: '',
      points: [10, 0, 8, 2, 6, 4, 5, 5],
      chartType: 'Spline',
      seriesColor: '#6fcd98',
      colorInputIsSupported: null,
      animationDuration: 1000,
      updateArgs: [true, true, {duration: 1000}],
      chartOptions: {
        chart: {
          type: 'spline'
        },
        title: {
          text: 'Sin chart'
        },
        series: [{
          data: [10, 0, 8, 2, 6, 4, 5, 5],
          color: '#6fcd98'
        }]
      }
    }
  },
  created () {
    let i = document.createElement('input')
    i.setAttribute('type', 'color');
    (i.type === 'color') ? this.colorInputIsSupported = true : this.colorInputIsSupported = false
  },
  watch: {
    title (newValue) {
      this.chartOptions.title.text = newValue
    },
    points (newValue) {
      this.chartOptions.series[0].data = newValue
    },
    chartType (newValue) {
      this.chartOptions.chart.type = newValue.toLowerCase()
    },
    seriesColor (newValue) {
      this.chartOptions.series[0].color = newValue.toLowerCase()
    },
    animationDuration (newValue) {
      this.updateArgs[2].duration = Number(newValue)
    }
  }
}
</script>

<style scoped>
input[type="color"]::-webkit-color-swatch-wrapper {
  padding: 0;
}
#colorPicker {
  border: 0;
  padding: 0;
  margin: 0;
  width: 30px;
  height: 30px;
}
.numberInput {
  width: 30px;
}
</style>
