<template>
  <div id="app2">
    <Weather/>
    <div id="chart" ref="barchart"></div>
  </div>
</template>

<script>
import Weather from './components/Weather.vue'


export default {
  name: 'app2',
  components: {
    Weather
  },
  data(){
    return{
  }
    }
   
}
</script>

<style>
#app2 {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

}

</style>
