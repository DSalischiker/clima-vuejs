<template>
  <div class="search-container">
    <input
      @keyup.prevent="keymonitor"
      v-model="cityInput"
      placeholder="Ingrese una ciudad"
      type="text"
      name="Search"
    />
    <button type="submit" @click="callAPI">
      <i class="ri-search-line"></i>
    </button>
  </div>
</template>

<script>
import axios from "axios";
import "remixicon/fonts/remixicon.css";
export default {
  name: "Search",
  data() {
    return {
      cityInput: "",
      BASE_URL: "https://api.openweathermap.org/data/2.5/weather?q=",
      apiKey: "d2c32268a991beb3f9c9a36c1329a18d",
    };
  },
  computed: {
    getURL() {
      return `${this.BASE_URL}${this.cityInput}&units=metric&appid=${this.apiKey}`;
    },
  },
  methods: {
    callAPI() {
      this.$emit("loadingData");
      axios
        .get(this.getURL)
        .then((response) => {
          console.log(response.data);
          //timeOut para simular loading

          setTimeout(() => {  this.$emit("showData", response.data); }, 1500);
        })
        .catch((error) => console.error(error))
        .then(() => console.log("hice el get"));
      /* this.cityInput = ''; */
    },
    keymonitor: function (event) {
      console.log(event.key);
      if (event.key == "Enter") {
        this.callAPI();
      }
    },
  },
};
</script>

<style lang="scss" scoped></style>
