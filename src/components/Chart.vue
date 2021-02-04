<template>
  <div id="app">
  <div id="shrink">
    <div id="chart" ref="barchart"></div>
    </div>
  </div>
</template>

<script>
import ApexCharts from 'apexcharts'
import data from '../assets/weather.json'
export default {
  name: 'app',
  data(){
      return{
          myJson: data,
          day:null,
          xvalues:null
      }
  },
    methods: {
    getDay: function () {
    var d = new Date();
    var weekday = new Array(7);
    var newWeekdays = new Array();
    weekday[0] = "Sunday";
    weekday[1] = "Monday";
    weekday[2] = "Tuesday";
    weekday[3] = "Wednesday";
    weekday[4] = "Thursday";
    weekday[5] = "Friday";
    weekday[6] = "Saturday";
  this.day = weekday[d.getDay()];
  var currentDay = d.getDay();
    for(var i = 0; i < 7; i++){
      if(currentDay == 6){
            newWeekdays.push(weekday[currentDay]);
            currentDay = 0;
        }else if(currentDay < 6){
            newWeekdays.push(weekday[currentDay]);
            currentDay++;
        }
    }
        this.xvalues = newWeekdays;
        console.log(this.xvalues);
        console.log(newWeekdays);
        }
    },
     beforeMount(){
      this.getDay()
    },
  mounted: function() {
    const chart = new ApexCharts(this.$refs.barchart, {
      chart: {
        type: 'line',
        height: 400
      },
      series: [
            {
              name: "High Temperature",
              data: [28, 29, 33, 36, 32, 32, 33]
            },
            {
              name: "Low Temperature",
              data: [12, 11, 14, 18, 17, 13, 13]
            }
          ],
          chartOptions: {
            chart: {
              height: 350,
              type: 'line',
              dropShadow: {
                enabled: true,
                color: '#000',
                top: 18,
                left: 7,
                blur: 10,
                opacity: 0.2
              },
              toolbar: {
                show: false
              }
            },
            colors: ['#77B6EA', '#545454'],
            dataLabels: {
              enabled: true,
            },
            stroke: {
              curve: 'smooth'
            },
            title: {
              text: 'Average High & Low Temperature',
              align: 'left'
            },
            grid: {
              borderColor: '#e7e7e7',
              row: {
                colors: ['#f3f3f3', 'transparent'], // takes an array which will be repeated on columns
                opacity: 0.5
              },
            },
            markers: {
              size: 1
            },
            xaxis: {
                
labels: {
    formatter: function () {
      return ["Saturday","Saturday","Saturday","Saturday","Saturday","Saturday","Saturday"];
    }
  }
                
            },
            yaxis: {
              title: {
                text: 'Temperature'
              },
              min: 5,
              max: 40
            },
            legend: {
              position: 'top',
              horizontalAlign: 'right',
              floating: true,
              offsetY: -25,
              offsetX: -5
            }
          }
    })

    chart.render();
    chart.updateSeries([{
  name: 'High Temperature',
  data: this.myJson.forecasts.high
},
{
  name: 'Low Temperature',
  data: this.myJson.forecasts.low
}])


  }
}
</script>
<style>
#shrink{
    width:84%;
    padding-left:98px;
}
</style>