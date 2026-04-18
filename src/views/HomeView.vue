<template>
    <div class="container mt-4">
        <h2 class="text-center mb-4">Weather App</h2>
      
        <div v-if="errorMsg"
             class="alert alert-danger alert-dismissible fade show">
            {{ errorMsg }}
            <button type="button"
                    class="close"
                    @click="errorMsg = null">
                    &times;
            </button>
        </div>
        <SearchBar @search="fetchWeather"></SearchBar>  <!--Equal to @search="fetchWeather($event)"-->
         <div v-if="loading" class="text-center">
            <div class="spinner-border text-primary"></div>
         </div>   
        <CurrentWeather v-if="weather" :weather="weather"></CurrentWeather>
        <HourlyForecast v-if="weather" :hourly="weather.hourly"></HourlyForecast>
        <WeatherChart v-if="weather" :hourly="weather.hourly"></WeatherChart>

    </div>
  

</template>
<script>
import axios from 'axios';
import SearchBar from '@/components/SearchBar.vue';
import CurrentWeather from '@/components/CurrentWeather.vue';
import HourlyForecast from '@/components/HourlyForecast.vue';
import WeatherChart from '@/components/WeatherChart.vue';



export default{
    components:{
        SearchBar,
        CurrentWeather,
        HourlyForecast,
        WeatherChart
    },
    data(){
        return{
            weather:null,
            loading:false,
            errorMsg:null
        }
    },
    methods:{
        async fetchWeather(city){
            try{
                this.loading=true;
                this.errorMsg=null;

                if(!city || city.trim() === ""){
                    this.errorMsg="Please enter a city name";
                    return;
                }
            const geoRes=await axios.get(`https://geocoding-api.open-meteo.com/v1/search?name=${city}`);
            console.log(geoRes.data);

            const {latitude,longitude}=geoRes.data.results[0];

            const weatherRes=await axios.get(`https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&current=temperature_2m,wind_speed_10m&hourly=temperature_2m`);
            // this.weather=weatherRes.data;
            //Hourly forecast
            this.weather={
                current:weatherRes.data.current,
                hourly:weatherRes.data.hourly.time.map((t,i)=>({
                    time:t,
                    temp:weatherRes.data.hourly.temperature_2m[i]
                }))
            }

         }catch(error){
            this.errorMsg="Something went wrong";
        }finally{
            this.loading=false;
        }
    }
}
}
</script>