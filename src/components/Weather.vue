
<template>
<div class="page-content page-container" id="app">
    <div class="padding">
        <div class="row container d-flex justify-content-center">
            <div class="col-lg-10 grid-margin stretch-card">
                <!--weather card-->
                <div class="card card-weather">
                    <div class="card-body">
                        <div class="weather-date-location">
                            <h3>{{day}}</h3>
                            <p class="text-gray"> <span class="weather-date">{{datetime}}</span> <span class="weather-location">{{myJson.location.city}}, {{myJson.location.region}}, {{myJson.location.country}}</span> </p>
                       <div class="col-md-4">
                        <select @change="cascade" class="form-control">
  <option value="1" selected="selected">Temperature</option>
  <option value="2">Wind Speed</option>
  <option value="3">Humidity</option>
  <option value="4">Pressure</option>
  <option value="5">Sunrise/Sunset</option>
</select>
</div>
                        </div>
                        <div class="weather-data d-flex">
                            <div class="mr-auto" v-if="showElement == 1">
                                <h4 class="display-3">{{myJson.current_observation.condition.temperature}} <span class="symbol">°</span>F</h4>
                                <p> {{myJson.current_observation.condition.text}} </p>
                            </div>
                            <div class="mr-auto" v-if="showElement == 2">
                                <h4 class="display-3">{{myJson.current_observation.wind.speed}} m/h</h4>
                                <p> chill: {{myJson.current_observation.wind.chill}} <br/> direction: {{myJson.current_observation.wind.direction}} <span class="symbol">°</span></p>
                            </div>
                            <div class="mr-auto" v-if="showElement == 3">
                                <h4 class="display-3">{{myJson.current_observation.atmosphere.humidity}}%</h4>
                                
                            </div>
                            <div class="mr-auto" v-if="showElement == 4">
                                <h4 class="display-3">{{myJson.current_observation.atmosphere.pressure}} mm Hg </h4>
                            </div>
                            <div class="mr-auto" v-if="showElement == 5">
                                <h4 class="display-3">{{myJson.current_observation.astronomy.sunrise}} </h4>
                                <p>Sunrise</p>
                                <h4 class="display-3">{{myJson.current_observation.astronomy.sunset}} </h4>
                                <p>Sunset</p>
                            </div>
                            
                        </div>
                    </div>
                    
                </div>
                <!--weather card ends-->
            </div>
            
        </div>
        <chart/>
    </div>
    
</div>  
</template>

<script>
import data from '../assets/weather.json'
import chart from './Chart.vue'

export default {
    components: {
        chart
    },
  data(){
              return{
                  myJson: data,
                  day:null,
                  datetime:null,
                    name: '',
                    showElement:1
              }
          },
          
           methods: {
               cascade: function(e){
                   this.showElement = e.target.value;
               },
    getDay: function () {
    var d = new Date();
    var weekday = new Array(7);
    weekday[0] = "Sunday";
    weekday[1] = "Monday";
    weekday[2] = "Tuesday";
    weekday[3] = "Wednesday";
    weekday[4] = "Thursday";
    weekday[5] = "Friday";
    weekday[6] = "Saturday";
  this.day = weekday[d.getDay()];

    const monthNames = ["January", "February", "March", "April", "May", "June",
    "July", "August", "September", "October", "November", "December"
    ];

  this.datetime = d.getDate() + ", "
                + (monthNames[d.getMonth()])  + " " 
                + d.getFullYear()
    }
  },
  beforeMount(){
      this.getDay()
    }        
}


</script>
    
<style>
.stretch-card>.card {
    width: 100%;
    min-width: 100%
}

body {
    background-color: #f9f9fa
}

.flex {
    -webkit-box-flex: 1;
    -ms-flex: 1 1 auto;
    flex: 1 1 auto
}

@media (max-width:991.98px) {
    .padding {
        padding: 1.5rem
    }
}

@media (max-width:767.98px) {
    .padding {
        padding: 1rem
    }
}

.padding {
    padding: 5rem
}

.grid-margin,
.purchace-popup>div {
    margin-bottom: 25px
}

.card {
    border: 0;
    border-radius: 2px
}

.card-weather {
    background: #e1ecff;
    background-image: linear-gradient(to left bottom, #d6eef6, #dff0fa, #e7f3fc, #eff6fe, #f6f9ff)
}

.card {
    position: relative;
    display: flex;
    flex-direction: column;
    min-width: 0;
    word-wrap: break-word;
    background-color: #fff;
    background-clip: border-box;
    border: 1px solid rgba(0, 0, 0, 0.125);
    border-radius: 0.25rem
}

.card-weather .card-body:first-child {
    background: url(https://res.cloudinary.com/dxfq3iotg/image/upload/v1557323760/weather.svg) no-repeat center;
    background-size: cover
}

.card .card-body {
    padding: 1.88rem 1.81rem
}

.card-body {
    flex: 1 1 auto;
    padding: 1.25rem
}

.card-weather .weather-date-location {
    padding: 0 0 38px
}

.h3,
h3 {
    font-size: 1.56rem
}

.h1,
.h2,
.h3,
.h4,
.h5,
.h6,
h1,
h2,
h3,
h4,
h5,
h6 {
    font-family: "Poppins", sans-serif;
    font-weight: 500
}

.text-gray,
.card-subtitle,
.new-accounts ul.chats li.chat-persons a p.joined-date {
    color: #969696
}

p {
    font-size: 13px;
}

.text-gray,
.card-subtitle,
.new-accounts ul.chats li.chat-persons a p.joined-date {
    color: #969696
}

.card-weather .weather-data {
    padding: 0 0 4.75rem
}

.mr-auto,
.mx-auto {
    margin-right: auto !important
}

.display-3 {
    font-size: 2.5rem
}

.card-weather .card-body {
    background: #ffffff
}

.card-weather .weakly-weather {
    background: #ffffff;
    overflow-x: auto
}

.card-weather .weakly-weather .weakly-weather-item {
    flex: 0 0 14.28%;
    border-right: 1px solid #f2f2f2;
    padding: 1rem;
    text-align: center
}

.mb-0,
.my-0 {
    margin-bottom: 0 !important
}

.card-weather .weakly-weather .weakly-weather-item i {
    font-size: 1.2rem
}
</style>