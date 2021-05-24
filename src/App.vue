<template>
  <div id="app" :class="appclass">
    <main>
      <!---search-bar-->

      <div class="search-bar">
        <input type="text" @keyup.enter="weather()" v-model="city_name" />
      </div>
      <div class="button"><button @click="weather()">Weather</button></div>

      <!----location---->
      <div class="content" v-if="typeof weathe.main != 'undefined'">
        <div class="location">
          <h3>{{ weathe.name }}, {{ weathe.sys.country }}</h3>
        </div>
        <div class="location">
          <h3>{{ dateBuilder() }}</h3>
        </div>
        <!---weater box---->
        <div class="weater">
          <div class="temp">
            <h1>{{ Math.round(weathe.main.temp) }}°c</h1>
          </div>
          <div class="weatertext">
            <h1>{{ weathe.weather[0].main }}</h1>
            <img :src="icon" :alt="weathe.weather[0].main" />
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
      api_key: "5a1b831eb88c7c57765fa1ce63eee8e5",
      url: "https://api.openweathermap.org/data/2.5/",
      city_name: "Baghdad",
      icon: "",
      alt: "",
      appclass: "",
      weathe: {},
    };
  },
  methods: {
    weather: function() {
      fetch(
        `${this.url}weather?q=${this.city_name}&units=metric&APPID=${this.api_key}`
      )
        .then((res) => {
          return res.json();
        })
        .then(this.setResults);
    },
    setResults(results) {
      this.weathe = results;
      const icon = this.weathe.weather[0].icon;
      this.icon = `http://openweathermap.org/img/w/${icon}.png`;
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

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
#app {
  width: 100vw;
  height: 100vh;
  background: linear-gradient(
    to right,
    rgba(78, 42, 209, 0.14),
    rgba(0, 92, 230, 0.4)
  );
}
main {
  width: 100%;
  height: 100%;
  margin: auto;
  background: linear-gradient(
    to right,
    rgba(0, 0, 0, 0.267),
    rgba(0, 0, 0, 0.205)
  );
  box-shadow: 4px 4px 8px rgba(78, 42, 209, 0.5),
    -4px -4px 8px rgba(0, 92, 230, 0.4);
}
.search-bar {
  width: 100%;
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.search-bar input {
  width: 90%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}
.search-bar input:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.button {
  width: 100%;
  height: 80px;
  display: flex;
  justify-content: center;
}
.button button {
  margin: 10px;
  padding: 10px;
  background: none;
  border: none;
  cursor: pointer;
  border: 1px solid #fff;
  font-size: 24px;
  color: #fff;
  font-family: Georgia, "Times New Roman", Times, serif;
}
.button button:hover {
  background: #000;
}
/*location*/
.location {
  width: 100%;
  height: 50px;
  text-align: center;
}
.location h3 {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.weater {
  width: 100%;
  height: 150px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.weater .temp {
  padding: 10px 15px;
  color: #fff;
  font-size: 22px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weatertext {
  width: 100%;
  height: 80px;
}
.weatertext h1 {
  width: 50%;
  float: left;
  display: flex;
  justify-content: flex-end;
  font-family: "Courier New", Courier, monospace;
  color: #000;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weatertext img {
  width: 80px;
}
</style>
