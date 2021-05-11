<template>
  <div>
    <input v-model="cityInput" type="text" name="" id="" />
    <button type="submit" @click="callAPI">Buscar</button>
  </div>
</template>

<script>
import axios from "axios";
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
      return "" + this.BASE_URL + this.cityInput + "&units=metric&appid=" + this.apiKey;
    },
  },
  methods: {
    callAPI() {
      axios.get(this.getURL)
        .then((response) => {
          console.log(response.data);
        })
        .catch((error) => console.error(error))
        .then(() => console.log("hice el get"));
      this.cityInput = '';
    },
  },
};
</script>

<style lang="scss" scoped></style>
