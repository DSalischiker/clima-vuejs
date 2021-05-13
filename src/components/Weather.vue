<template>
  <div class="weather-container" :class="[itsDayTime ? 'day' : 'night', isHot ? 'hot' : 'cold']">
    <div class="components-container">
      <p class="date">{{ currentDate }}</p>
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
      return this.getHour() < "14:00";
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

<style lang="scss" scoped></style>
