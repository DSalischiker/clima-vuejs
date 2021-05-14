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

<style lang="scss" scoped>
.search-container{
  height: 10%;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 80%;
  display: flex;
  align-items: center;
  margin: 0 auto;
  gap: 1em;
  input[type=text]{
    position: relative;
    padding: 15px 20px 15px 20px;
    width: 70%;
    color: #525252;
    text-transform: uppercase;
    text-align: left;
    font-size: 10px;
    font-weight: 400;
    letter-spacing: 2px;
    border: none;
    border-radius: 8px;
    background: linear-gradient(to right, #FFFFFF 0%,#464747 #F9F9F9 100%);
    transition: all 0.2s ease-in-out;
    outline: none;
    &:hover{
      font-size: 12px;
      transition: all 0.2s ease-in-out;
    }
    /* &:focus{
      border: 3px solid blueviolet;
      transition: all 0.2s ease-in-out 0.5s;
    } */
  }
  button{
    padding: 10px;
    border: none;
    border-radius: 8px;
    outline: none;
    font: inherit;
    color: inherit;
    background-color: rgba($color: #dfdfdf, $alpha: 0.3);
    letter-spacing: 3px;
    font-weight: 400;
    text-transform: uppercase;
    cursor: pointer;
    transition: all 0.2s ease-in-out;
    &:hover{
      background-color: rgba($color: #dfdfdf, $alpha: 0.6);
      transition: all 0.2s ease-in-out;
    }
  }
  i{
    font-size: 20px;
    position: relative;
    color: white;
  }
}

</style>
