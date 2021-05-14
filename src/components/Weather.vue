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

<style lang="scss" scoped>
.weather-container {
  width: 80%;
  max-width: 600px;
  height: auto;
  padding: 2em;
  border-radius: 8px;
  margin: auto;
  &.day {
    background: #56ccf2; /* fallback for old browsers */
    background: -webkit-linear-gradient(
      to top,
      #2f80ed,
      #56ccf2
    ); /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(
      to top,
      #2f80ed,
      #56ccf2
    ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  }
  &.night {
    background: #0f2027; /* fallback for old browsers */
    background: -webkit-linear-gradient(
      to top,
      #2c5364,
      #203a43,
      #0f2027
    ); /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(
      to top,
      #2c5364,
      #203a43,
      #0f2027
    ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  }
  &.hot {
    background: #ff512f; /* fallback for old browsers */
    background: -webkit-linear-gradient(
      to top,
      #f09819,
      #ff512f
    ); /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(
      to top,
      #f09819,
      #ff512f
    ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  }
  &.cold {
    background: #24c6dc; /* fallback for old browsers */
    background: -webkit-linear-gradient(
      to top,
      #514a9d,
      #24c6dc
    ); /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(
      to top,
      #514a9d,
      #24c6dc
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
    margin-bottom: 2em;
    font-size: 12px;
    letter-spacing: 3px;
    font-weight: 400;
    text-transform: uppercase;
    height: 10%;
  }
}
</style>
