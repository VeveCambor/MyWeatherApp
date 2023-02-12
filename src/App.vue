<template>
  <div id="app">
    <main>
     <h1>Weather App</h1>
     <div class="weather-container">
    <div class="search-box">
        <input type="text" 
        class="search-bar" 
        placeholder="Search.." 
        v-model="query"
        @keyup="fetchWeather"
        />
    </div>
    <W-button @click="fetchCWeather"/>
    <transition name="bounce">
      <div class="weather-wrap" v-if="typeof weather.main !== 'undefined'">
        <div class="location-box">
        <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
        <div class="date">{{ dateBuilder() }}</div>
      </div>

      <div class="weather-box">
        <div class="temp">{{ Math.round(weather.main.temp) }}°c</div> 
        <div class="weather">{{ weather.weather[0].main }}
        <img class="icon" :src="imgPath" alt="Weather icons">
      </div>
        </div>
       </div>
    </transition>
    </div>
  </main>
 </div>
</template>

<script>
import WButton from './components/WButton.vue'

const weatherIcons = {
     Fog: 'Mist',
     Mist: 'Mist',
     Clear: 'Clear',
     Rain: 'Rain',
     Snow: 'Snow',
     Clouds: 'Clouds',
     ThunderStorm: 'Storm' 
   }
 
export default {
  name: 'app',
  data () {
    return {
      api_key: '8df2d60812c3cd4d6c667a9fdd5218ec',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}, 
    } 
  },
  computed: {
    imgPath() {
      return './src/assets/icon/' + weatherIcons[this.weather.weather[0].main] + '.png'
    }
  },
  methods: {
    fetchWeather (e) {
      if (e.key === "Enter") {
        fetch (`${this.url_base}weather?q=${this.query}&units=metric&appid=${this.api_key}`)
        .then(res => {
        return res.json();
      }).then(this.setResults);
     }
    },
    fetchCWeather (e) {    
        fetch (`${this.url_base}weather?q=${this.query}&units=metric&appid=${this.api_key}`)
        .then(res => {
        return res.json();
      }).then(this.setResults);    
    },
    setResults (results) {
      this.weather = results;
    },
    dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      

      return `${day} ${date} ${month} ${year}`
    } 
   },
    components: { WButton }
  }

</script>



<style>
  
</style>
