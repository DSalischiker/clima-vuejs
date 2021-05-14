<template>
  <div class="weather-container" :class="[itsDayTime ? 'day' : 'night', isHot ? 'hot' : 'cold']">
    <div class="components-container">
      <span class="date">{{ currentDate }}</span>
      <!-- <span class="date">{{getHour()}}</span> -->
      <Search class="search" @showData="showData" @loadingData="loadingData"  />
      <Data
        class="data"
        :weatherData="weatherData"
        :loadingData="loadingState"
      />
    </div>
  </div>
</template>

<script>
import Search from "@/components/Search.vue";
import Data from "@/components/Data.vue";
import moment from "moment";
export default {
  name: "Weather",
  components: {
    Search,
    Data,
  },
  data() {
    return {
      weatherData: {},
      loadingState: false,
      isHot: null,
    };
  },
  computed: {
    currentDate() {
      return moment().format("dddd Do MMMM");
    },
    itsDayTime() {
      return this.getHour() < "19:00";
    },
  },
  methods: {
    getHour(){
      const today = new Date();
      const time =
        today.getHours() + ":" + today.getMinutes();
        return time;
    },
    showData(data) {
      this.weatherData = data;
      this.loadingState = false;
      this.isHot = this.weatherData.main.temp >= 18;
    },
    loadingData() {
      this.loadingState = true;
      console.log("loadingtrue");
    },
  },
};
</script>

<style lang="scss" scoped>
.weather-container {
  width: 80%;
  max-width: 600px;
  height: auto;
  padding: 2em;
  border-radius: $roundedBorder;
  margin: auto;

  /* Backgrounds */
  &.day {
    background: $dayColorOne; /* fallback for old browsers */
    background: -webkit-linear-gradient(
      to top,
      $dayColorTwo,
      $dayColorOne
    ); /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(
      to top,
      $dayColorTwo,
      $dayColorOne
    ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  }
  &.night {
    background: $nightColorOne; /* fallback for old browsers */
    background: -webkit-linear-gradient(
      to top,
      $nightColorTwo,
      $nightColorThree,
      $nightColorOne
    ); /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(
      to top,
      $nightColorTwo,
      $nightColorThree,
      $nightColorOne
    ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  }
  &.hot {
    background: $hotColorOne; /* fallback for old browsers */
    background: -webkit-linear-gradient(
      to top,
      $hotColorTwo,
      $hotColorOne
    ); /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(
      to top,
      $hotColorTwo,
      $hotColorOne
    ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  }
  &.cold {
    background: $coldColorOne; /* fallback for old browsers */
    background: -webkit-linear-gradient(
      to top,
      $coldColorTwo,
      $coldColorOne
    ); /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(
      to top,
      $coldColorTwo,
      $coldColorOne
    ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  }

}
.components-container {
  max-width: 800px;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  margin: auto;

  .date {
    font-size: $pSize;
    letter-spacing: $textSpacing;
    font-weight: $regularWeight;
    text-transform: $textTransform;
    height: 10%;

    &:last-of-type{
      margin-bottom: $marginBottom;
    }
  }
}
</style>
