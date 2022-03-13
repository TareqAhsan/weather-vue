<template>
  <div id="app">
    <div class="container d-flex py-3">
      <input
        type="text"
        v-model="query"
        class="form-control me-2"
        placeholder="search city name"
      />
      <button class="btn btn-primary" v-on:click="fetchWeather">search</button>
    </div>
    <div v-if="weather.main" class="container">
      <div class="d-flex justify-content-center align-items-center flex-column p-3">
        <h3>{{ weather.name }}, {{ weather.sys.country }}</h3>
        <h3>{{ weather.main.temp }}°C</h3>
        <h4>{{ weather.weather[0].main }}</h4>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      api_key: "a9246e3abab3c3b7711a9f172a15d900",
      query: "",
      url: "https://api.openweathermap.org/data/2.5/",
      weather: {},
    };
  },
  methods: {
    fetchWeather() {
      fetch(
        `${this.url}weather?q=${this.query}&units=metric&appid=${this.api_key}`
      )
        .then((res) => res.json())
        .then((result) => {
          this.setResult(result);
          console.log(result);
        });
    },
    setResult(result) {
      // console.log(result);
      this.weather = result;
    },
  },
};
</script>

<style>
#app {
  background-image: url("./assets/bg-image/bg.jpeg");
  height: 100vh;
  background-size: cover;
  background-position: fixed;
}
.flex-column{
  background-color:rgba(231, 231, 227,0.5);
  width: 50%;
  margin: 0 auto;
  border-radius: 20px;
}
</style>
