<template>
  <div id="app">
    <Header />
    <div class="container">
      <Alert :alertColor="alertColor" :alertMessage="alertMessage" />
      <Search @get-weather="getWeather" />
      <Loader :visible="loaderVisible" />
      <WeatherCard
        :temp="temp"
        :tempMin="tempMin"
        :tempMax="tempMax"
        :desc="desc"
        :humid="humid"
        :precip="precip"
        :city="city"
        :country="country"
        :imgSrc="imgSrc"
        :imgAlt="imgAlt"
      />
    </div>
  </div>
</template>

<script>
import API_KEY from './env';
import Header from './components/layout/Header';
import Alert from './components/Alert';
import Search from './components/Search';
import WeatherCard from './components/WeatherCard';
import Loader from './components/Loader';

export default {
  name: 'App',

  components: {
    Header,
    Alert,
    Search,
    WeatherCard,
    Loader
  },

  methods: {
    getWeather({ city, country }) {
      // Show loader right before making request
      this.loaderVisible = 'visible';

      setTimeout(() => {
        fetch(
          `https://api.openweathermap.org/data/2.5/find?q=${city},${country}&units=metric&appid=${this.api_key}`
        )
          .then((res) => res.json())
          .then((data) => {
            // Hide loader after fetch is done
            this.loaderVisible = '';

            const _icon = data.list[0].weather[0].icon;

            this.imgSrc = `http://openweathermap.org/img/wn/${_icon}@2x.png`;
            this.imgAlt = data.list[0].weather[0].description;

            this.temp = Math.round(data.list[0].main.temp).toString() + ' °C';
            this.tempMin = Math.round(data.list[0].main.temp_min).toString() + '°';
            this.tempMax = Math.round(data.list[0].main.temp_max).toString() + '°';
            this.city = data.list[0].name + ',';
            this.country = data.list[0].sys.country;

            this.desc = data.list[0].weather[0].description;
            this.humid = `Humidity: ${data.list[0].main.humidity.toString()}%`;
            this.precip =
              'Precipitation: ' +
              (data.list[0].rain ? data.list[0].rain['1h'] * 100 : '0') +
              '%';
          })
          .catch((err) => {
            console.log(err);

            // Show alert
            this.alertColor = 'danger';
            this.alertMessage = 'Data not found. Please check your input...';
            // Hide alert after 3 sec
            setTimeout(() => {
              this.alertColor = '';
              this.alertMessage = '';
            }, 3000);
          });
      }, 800);
    }
  },

  data() {
    return {
      imgSrc: '',
      imgAlt: '',

      temp: '',
      tempMin: '',
      tempMax: '',
      city: '',
      country: '',

      desc: '',
      humid: '',
      precip: '',

      loaderVisible: '',
      alertColor: '',
      alertMessage: '',
      api_key: API_KEY
    };
  }
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap');

$colors: (
  primary: #523fa8,
  primary-alt: #ee65fa,
  secondary: #f38f1d
);

*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins', Arial, Helvetica, sans-serif;
}

#app {
  height: 100vh;
  background: linear-gradient(
    135deg,
    map-get($colors, primary) 0%,
    map-get($colors, primary-alt) 90%
  );

  animation: moveBG 16s ease-in-out infinite;
  animation-fill-mode: forwards;

  ::selection {
    background-color: map-get($colors, secondary);
    color: white;
  }
}

.container {
  margin: 0 1em;
}

.btn {
  cursor: pointer;
  outline: none;
  border: none;
  border-radius: 0.5em;
  padding: 0.6em 1.2em;
  margin: 0.3em 0 1.5em 0;

  background-color: white;
  color: map-get($colors, secondary);
  font-weight: 500;
  font-size: 1.1em;

  transition: 0.3s ease;
}
.btn:hover {
  box-shadow: 0px 16px 20px -11px rgba(0, 0, 0, 0.255);
  transform: translateY(-10%);
}
.btn:active {
  box-shadow: none;
  background-color: map-get($colors, secondary);
  color: white;
}

/********* ANIMATIONS *********/
@keyframes moveBG {
  0% {
    background-size: 100%;
  }
  50% {
    background-size: 400%;
  }
  100% {
    background-size: 100%;
  }
}
</style>
