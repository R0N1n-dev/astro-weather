<template>
  <div class="container">
    <h4 class="heading">Weather Search</h4>
    <div class="search">
      <input
        class="input"
        type="text"
        v-model="query"
        @keypress="getWeather"
        placeholder="Enter city"
      />
    </div>
    <div
      class="notification is-dark mt-4"
      v-if="typeof weather.main != 'undefined'"
    >
      <div class="image">
        <img
          :src="
            `http://openweathermap.org/img/wn/` +
            weather.weather[0].icon +
            `@2x.png`
          "
          alt="weather-icon"
          class="icon"
        />
      </div>
      <div class="card-text">
        <p class="date">{{ dateBuilder() }}</p>
        <h2>{{ weather.name }}, {{ weather.sys.country }}</h2>
        <span>{{ weather.main.temp }}°C</span> <br />
        <span
          >{{ weather.weather[0].main }}:
          {{ weather.weather[0].description }}</span
        ><br />
        <span></span>
      </div>
      <div class="card-stats">
        <div class="stats">
          <div class="type">low:</div>
          <div class="value">{{ weather.main.temp_min }}°C</div>
        </div>
        <div class="stats border">
          <div class="type">high:</div>
          <div class="value">{{ weather.main.temp_max }}°C</div>
        </div>
        <div class="stats">
          <div class="type">humidity</div>
          <div class="value">{{ weather.main.humidity }}%</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      key: "e6aea0474f2b4a44e1f0c3ddadc0b4ed",
      base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    getWeather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.base}weather?q=${this.query}&units=metric&APPID=${this.key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
      this.query = "";
    },
    dateBuilder() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;
    },
  },
};
</script>

<style scoped>
.icon {
  width: 80px;
  height: 80px;
}
</style>
