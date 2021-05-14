<template>
    <div><p>Data</p></div>
  <div>
    <div v-if="loadingData">
      <div class="lds-ellipsis">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
      </div>
    </div>
    <div v-if="!loadingData && cityName" class="data-container" :class="{ active: active }">
      <div class="data-container-inner">
        <div class="weather-data-container">
          <div class="weather-data-inner">
            <i
              style="font-size: 72px"
              :class="getIconClass(this.weatherCondition)"
            ></i>
            <p class="weather-description">
              {{ this.weatherData.weather[0].description }}
            </p>
          </div>
          <div class="weather-data-inner">
            <h1 class="main-temperature">
              {{ this.mainData.temp | roundNumber | temperature }}
            </h1>
            <div class="weather-detail-container">
              <div class="weather-detail-inner">
                <span class="weather-detail">{{
                  this.mainData.temp_min | roundNumber | temperature
                }}</span>
                <span class="weather-detail"
                  ><i class="ri-arrow-down-s-line"></i
                ></span>
              </div>
              <div class="weather-detail-inner">
              <span class="weather-detail">{{
                this.mainData.temp_max | roundNumber | temperature
              }}</span>
              <span class="weather-detail"
                ><i class="ri-arrow-up-s-line"></i
              ></span>
            </div>
            </div>
          </div>
        </div>
        <!-- Main temperature -->
        <h2 class="city-name">{{ this.cityName }}</h2>
      </div>
    </div>

    <div class="no-data" v-else v-show="!cityName && !loadingData">Esperando ciudad...</div>
  </div>
</template>

<script>
import "remixicon/fonts/remixicon.css";

export default {
    name: "Data",
}
  name: "Data",
  props: ["weatherData", "loadingData"],
  data() {
    return {};
  },
  computed: {
    cityName() {
      return this.weatherData.name;
    },
    mainData() {
      return this.weatherData.main;
    },
    weatherCondition() {
      return this.weatherData.weather[0].main;
    },
    active() {
      return this.weatherData != null;
    },
  },
  methods: {
    getIconClass(main) {
      if (main === "Clear") {
        return "ri-sun-line";
      } else if (main == "Thunderstorm") {
        return "ri-thunderstorms-line";
      } else if (main == "Drizzle" || main == "Rain") {
        return "ri-showers-line";
      } else if (main == "Snow") {
        return "ri-snowy-line";
      } else if (main == "Clouds") {
        return "ri-cloudy-line";
      } else {
        return "ri-sun-cloudy-line";
      }
    },
  },
  filters: {
    temperature(value) {
      return value ? value + "°C" : "";
    },
    roundNumber(value) {
      return value ? Math.round(value) : "";
    },
  },
};
</script>

<style lang="scss" scoped>

</style>