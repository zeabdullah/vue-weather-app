<template>
  <div class="weather-card">
    <div class="card">
      <div class="left">
        <img :src="imgSrc" :alt="imgAlt" />
        <h2 class="city">
          {{ city }}<span class="country"> {{ country }}</span>
        </h2>
        <p class="temp-main">{{ temp }}</p>
        <p class="minmax">
          <span class="min">{{ tempMin }}</span>
          <span class="max">{{ tempMax }}</span>
        </p>
      </div>

      <div class="right">
        <p class="desc">{{ desc }}</p>
        <p class="humid">{{ humid }}</p>
        <p class="precip">{{ precip }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WeatherCard',

  props: {
    imgSrc: String,
    imgAlt: String,

    temp: String,
    tempMin: String,
    tempMax: String,

    city: String,
    country: String,
    desc: String,
    humid: String,
    precip: String
  }
};
</script>
scss
<style lang="scss" scoped>
.card {
  display: flex;

  box-shadow: 0px 10px 18px -8px rgba(0, 0, 0, 0.28);
  transition: 0.3s ease;

  .left,
  .right {
    width: 100%;
    padding: 0.7em;
  }

  .left {
    color: white;
    background-color: #280038;
    border-right: 1px solid black;
    border-radius: 10px 0 0 10px;
    padding-top: 0;

    display: grid;
    place-content: center;
    justify-content: start;
    align-content: start;

    .city {
      text-transform: uppercase;
      letter-spacing: 0.04em;
      font-size: 2em;
    }
    .country {
      letter-spacing: 0px;
      font-size: 0.6em;
    }

    .temp-main {
      font-size: 2.5em;
    }

    .minmax {
      font-size: 1.1em;
      font-weight: 400;

      .min {
        color: rgb(39, 140, 255);
        padding-right: 0.5em;
      }
      .max {
        color: #f04400;
      }
    }
  }

  .right {
    background-color: #ffffff;
    border-radius: 0 10px 10px 0;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;

    p {
      padding: 0.15em 0 0.15em 0;
      letter-spacing: 0;
      font-size: 1.2em;
      font-weight: 300;
    }
    p.desc {
      font-size: 1.4em;
      text-transform: capitalize;
      font-weight: 600;
      margin-bottom: 2px;
    }
  }
}
</style>
