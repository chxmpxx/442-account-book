<template>
  <div class="graph">
    <img src="../assets/02.png">
    <br><br>
    <h1>Graph</h1>
    <br>

    <div class="chart">
      <VueApexCharts height="430" type="bar" :options="chartOptions" :series="series"/>
    </div>
    <br><br>
  </div>
</template>

<script>
import InputStore from '@/store/InputStore.js'
import VueApexCharts from "vue-apexcharts";
export default {
  components: { VueApexCharts },
  data(){
    return{
      inputs:[],
      inc: 3200,
      exp: -2350,
      income:[],
      expense:[],

      series: [
      {
        name: "Income",
        data: [0, 0, 3000, 3000, 3200]
      }, {
        name: "Expense",
        data: [250, 850, 850, 2350, 2350]
      }],
      chartOptions: {
        chart: {
          type: 'bar',
          height: 430
        },
        plotOptions: {
          bar: {
            horizontal: true,
            dataLabels: {
              position: 'top',
            },
          }
        },
        dataLabels: {
          enabled: true,
          offsetX: -6,
          style: {
            fontSize: '12px',
            colors: ['#4B4B4B']
          }
        },
        stroke: {
          show: true,
          width: 1,
          colors: ['#fff']
        },
        tooltip: {
          shared: true,
          intersect: false
        },
        xaxis: {
          categories: ["2021-06-06", "2021-06-15", "2021-06-31", "2021-07-01", "2021-07-15"],
        },
        fill: {
          colors: ['#F2939B', '#FFE0D8']
        },
        colors: ['#F2939B', '#FFE0D8']
      },
    }
  },
  created(){
    this.fetchInput()
  },
  methods:{
    fetchInput(){
      InputStore.dispatch('fetchData')
      this.inputs = InputStore.getters.inputs
      this.loopInput()
    },
    loopInput(){
      this.inputs.forEach((i) => {
        this.income.push(Number(i.inc));
        this.expense.push(Number(i.exp));
      });
      //this.series = this.income
    },
  },
}
</script>

<style lang="scss" scoped>
img{
display: block;
  margin-left: auto;
  margin-right: auto;
  width: 100%;
}
h1{
  color: #4B4B4B;
  font-size: 36px;
  background-color: #FFF6E5;
  border-style: dashed;
  border-width: 1.5px;
  border-radius: 15px;
  margin: 0em 30em 0em 2em;
  padding: 0.1em 3.5em 0.1em 0.5em;
}
.graph{
  background-color: #FFE0D8;
}
.chart{
  font-size: 0.5em;
  color: #4B4B4B;
  background-color: #FFF6E5;
  border-style: dashed;
  border-width: 1.5px;
  border-radius: 15px;
  margin: 0em 4.5em 0em 4.5em;
  padding: 0.5em 0 0.5em 0;
}
</style>