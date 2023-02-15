<template>
  <div id="container">
    <div id="search-box">
      <input id="search-input" type="text" placeholder="City" v-model="city" />
    </div>
    <button @click="getWeatherData">Get weather data</button>
    <select v-model="selectedUnit">
      <option value="metric">Metric</option>
      <option value="imperial">Imperial</option>
    </select>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "WeatherApp",
  data() {
    return {
      city: "",
      selectedUnit: "metric",
      weatherData: "",
    };
  },
  methods: {
    getWeatherData() {
      axios
        .get(
          "https://api.openweathermap.org/data/2.5/forecast?q=" +
            this.city +
            "&units=" +
            this.selectedUnit +
            "&appid=d19ef8e85125dd9558bd15f4d5fb8e8e"
        )
        .then((res) => {
          this.weatherData = res.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style scoped>
#container {
  display: flex;
  flex-direction: column;
}
#search-input {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
}
</style>
