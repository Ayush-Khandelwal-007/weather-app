<template>
  <div id="app" :class="typeof weather.main!== 'undefined' && weather.main.temp > 20 ?'warm':''">
    <main>
      <div class="search-box">
        <input
          type="text"
          class="search-bar"
          placeholder="Search for the desired city..."
          v-model="query"
          @keypress="keyDown"
        />
        <button><img :src='"./assets/search.svg"' class="search" v-on:click="fetchWeather"/></button>
      </div>
      <div class="weather-root" v-if="typeof weather.main != `undefined`">
        <div class="info-container">
          <div class="location">
            {{ weather.name }},{{countryName}}
            <span>( {{ weather.coord.lon }} , {{ weather.coord.lat }} )</span>
          </div>
          <div class="date">{{ today() }}</div>
        </div>
        <div class="weather-box">
          <div class="temp">
            <img class="icon" :src="iconSrc" />
            {{ Math.round(weather.main.temp * 10) / 10 }}°c
          </div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
      <div class="weather-root" v-if="error">
        <div class="weather-box">
          <div class="error">
            Oops No city with this name found.
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "593210a225d49521802201d5fd34bdd2",
      base_url: "https://api.openweathermap.org/data/2.5",
      query: "",
      weather: {temp:'data'},
      iconSrc: "",
      countryName:"",
      error:false,
    };
  },
  methods: {
    keyDown (e){
      if (e.key == "Enter") {
        this.fetchWeather();
      }
    },
    fetchWeather() {
        fetch(
          `${this.base_url}/weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((data) => {
            return data.json();
          })
          .then((results) => {
            console.log(results)
            this.weather = results;
            let regionNames = new Intl.DisplayNames(['en'], {type: 'region'});
            this.countryName=regionNames.of(results.sys.country);
            this.iconSrc = `http://openweathermap.org/img/wn/${results.weather[0].icon}@2x.png`;
          })
          .catch(error =>{
            console.log(error);
            this.error = true;
          });
    },
    today() {
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

<style>
* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
#app {
  background: url("./assets/coldBg.jpeg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: bottom;
  height: 100vh;
  transition: 0.6s;
}
#app.warm {
  background: url("./assets/hotBg.jpeg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: bottom;
  height: 100vh;
  transition: 0.6s;
}
main {
  min-height: 100vh;
  padding: 2rem;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0),
    rgba(0, 0, 0, 0.75)
  );
}
.search-box {
  width: 100%;
  margin: 2rem 0px;
  display: flex;
  justify-content: center;
}
.search-bar {
  display: block;
  width: 100%;
  max-width: 800px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 1rem;

  color: #010101;
  font-size: 1.25rem;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 0.5rem rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 1rem 0px 1rem 0px;
  transition: 0.6s;
}
.search-box .search-bar:focus {
  box-shadow: 0px 0px 1rem rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 0px 1rem 0px 1rem;
}
.info-container .location {
  color: #fff;
  font-size: 2rem;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location > span {
  font-size: 1rem;
}
.info-container .date {
  color: #fff;
  font-size: 1.25rem;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 0.75rem 1.55rem;
  color: #fff;
  font-size: 8rem;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 1rem;
  margin: 2rem 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  cursor: default;
}

.error{
  display: inline-block;
  padding: 0.75rem 1.55rem;
  color: #fff;
  font-size: 2rem;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 1rem;
  margin: 2rem 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  cursor: default;
}
.weather-box .weather {
  color: #fff;
  font-size: 3rem;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.icon {
  position: absolute;
  transform: translate(-60%, -53%) rotate(-38deg) scale(1.3);
}
.search {
  width:2rem;
  cursor: pointer;
  transform:rotateY(180deg);
}
button {
  background:rgba(0, 0, 0, 0.25);
  padding: 0.4rem 0.8rem;
  border-radius:5px;
  border: none;
  margin-left:1rem ;
}
</style>
