<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input
          type="text"
          class="text search-bar"
          placeholder="Search..."
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>

      <div class="weather-wrapper" v-if="typeof weather.main != 'undefined'">
        <div class="location">
          <h1>{{ weather.name }}, {{ weather.sys.country }}</h1>
          <p>{{ getDate() }}</p>
        </div>
        <div class="weather-box">
          <p class="temp">{{ Math.round(weather.main.temp) }} °c</p>
          <p class="weather">{{ weather.weather[0].main }}</p>
          <p class="weather">{{ weather.weather[0].description }}</p>
        </div>
      </div>
      <!-- <div style="color: white">
        {{ weather }}
      </div> -->
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "743ee6457923d2f6fa6e9d5eaeadcd5e",
      api_url: "http://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.api_url}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setWeather);
      }
    },
    setWeather(feth_results) {
      this.weather = feth_results;
    },
    getDate() {
      let date = new Date();
      const days = ["Sun", "Mon", "Tue", "Wed", "Thur", "Fri", "Sat"];
      const months = [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "Oct",
        "Nov",
        "Dec",
      ];
      let date_string = `${days[date.getDay()]}  ${date.getDate()}, ${
        months[date.getMonth()]
      } ${date.getFullYear()}`;
      return date_string;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat&display=swap");
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  background: url("./assets/raimond-klavins-unsplash.jpg") center/cover;
  background-position: bottom;
  transition: 0.4s;
  font-family: "Montserrat", sans-serif;
}
main {
  min-height: 100vh;
  padding: 2rem;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
}
.search-box {
  width: 100%;
  margin-bottom: 3rem;
}
.search-box .search-bar {
  width: 60%;
  display: block;
  margin: auto;
  padding: 15px;
  font-size: 1.2rem;
  appearance: none;
  border: none;
  outline: none;
  color: #006a94;
  background-color: rgba(255, 255, 255, 0.5);
  border-top-right-radius: 8px;
  border-bottom-left-radius: 8px;
  transition: 0.4s;
  text-align: center;
}
.search-bar:focus {
  background-color: rgba(255, 255, 255, 0.9);
  border-radius: 8px;
}
.location {
  color: white;
  text-align: center;
}
.location h1 {
  font-size: 2rem;
  font-weight: 500;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location p {
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
}
.weather-box {
  color: white;
  text-align: center;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .temp {
  font-size: 6rem;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-image: linear-gradient(
    to left,
    rgba(255, 255, 255, 0.15),
    rgba(255, 255, 255, 0.25)
  );
  display: inline-block;
  padding: 10px 25px;
  margin: 30px 0;
  border-radius: 1rem;
}
.weather-box .weather {
  font-size: 3rem;
  font-weight: 700;
  font-style: italic;
}
</style>