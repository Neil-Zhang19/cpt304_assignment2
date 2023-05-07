<!-- WeatherInfo.vue -->
<template>
    <div v-if="weather">
      <h3>Weather Information</h3>
      <p>Temperature: {{ weather.temperature }}°C</p>
      <p>Humidity: {{ weather.humidity }}</p>
      <p>Wind Speed: {{ weather.wind_speed }} m/s</p>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    props: {
      country: String,
      area: String,
      date: String,
    },
    data() {
      return {
        weather: null,
      };
    },
    watch: {
      area: {
        handler() {
          this.fetchWeatherInfo();
        },
      },
      date: {
        handler() {
          this.fetchWeatherInfo();
        },
      },
      country: {
        handler() {
          this.fetchWeatherInfo();
        },
      },
    },
    created() {
        if (this.area && this.date && this.country) {
            this.fetchWeatherInfo();
        }
    },
    methods: {
      async fetchWeatherInfo() {
        if (!this.area || !this.date) {
          return;
        }
  
        const options = {
          method: 'GET',
          url: 'https://weather-by-api-ninjas.p.rapidapi.com/v1/weather',
          params: {
            city: this.area,
            country: this.country, 
          },
          headers: {
            'X-RapidAPI-Key': '0d26327d82msh32aef66c29a4f2bp1e8a47jsne7d5a523895b',
            'X-RapidAPI-Host': 'weather-by-api-ninjas.p.rapidapi.com',
          },
        };
  
        try {
          const response = await axios.request(options);
          this.weather = {
            temperature: response.data.temp,
            humidity: response.data.humidity,
            wind_speed: response.data.wind_speed,
          };
        } catch (error) {
          console.error(error);
        }
      },
    },
  };
  </script>
  