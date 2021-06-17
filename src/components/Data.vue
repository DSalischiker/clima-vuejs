<template>
  <div>
    <!-- Loading animation -->
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

    <p class="no-data" v-else v-show="!cityName && !loadingData">Esperando ciudad..</p>
  </div>
</template>

<script>
import "remixicon/fonts/remixicon.css";

export default {
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
.data-container {
  height: 80%;
  transition: height 1s ease-in-out;

  .data-container-inner {
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin: 1em auto;
  }

  .weather-data-container {
    width: 100%;
    display: flex;
    margin: 0 auto;
  }

  .weather-data-inner {
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .main-temperature {
    margin: 0.5em auto 0.2em auto;
    padding: 0;
    font-size: 36px;
    font-family: $fontFamily;
    font-weight: $boldWeight;
  }

  .weather-description {
    font-size: $weatherDetailSize;
    letter-spacing: $textSpacing;
    font-weight: $regularWeight;
    text-transform: $textTransform;
    margin: 0.2em auto 0 auto;
    padding: 0;
  }

  .weather-detail-container {
    display: flex;
    justify-content: center;
    gap: $flexGap;
    align-items: center;
  }

  .weather-detail-inner {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .weather-detail {
    font-size: $weatherDetailSize+2px;
  }

  .city-name {
    font-size: $cityName;
    margin: 0.5em auto 0 auto;
    text-transform: $textTransform;
    letter-spacing: 6px;
    font-weight: $boldWeight;
  }
}

.no-data {
  margin-top: 2em;
  font-family: $fontFamily;
  text-transform: $textTransform;
  letter-spacing: $textSpacing;
  font-size: $pSize;
  font-weight: $regularWeight;
  animation: blink 2s infinite;
}
@keyframes blink {
  0% { opacity: 0; }
  50% { opacity: 1; }
  100% { opacity: 0; }
}
/* Loading animation */
.lds-ellipsis {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-ellipsis div {
  position: absolute;
  top: 33px;
  width: 13px;
  height: 13px;
  border-radius: 50%;
  background: #fff;
  animation-timing-function: cubic-bezier(0, 1, 1, 0);
}
.lds-ellipsis div:nth-child(1) {
  left: 8px;
  animation: lds-ellipsis1 0.6s infinite;
}
.lds-ellipsis div:nth-child(2) {
  left: 8px;
  animation: lds-ellipsis2 0.6s infinite;
}
.lds-ellipsis div:nth-child(3) {
  left: 32px;
  animation: lds-ellipsis2 0.6s infinite;
}
.lds-ellipsis div:nth-child(4) {
  left: 56px;
  animation: lds-ellipsis3 0.6s infinite;
}
@keyframes lds-ellipsis1 {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}
@keyframes lds-ellipsis3 {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(0);
  }
}
@keyframes lds-ellipsis2 {
  0% {
    transform: translate(0, 0);
  }
  100% {
    transform: translate(24px, 0);
  }
}

</style>
