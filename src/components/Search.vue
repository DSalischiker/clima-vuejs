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

          setTimeout(() => {
            this.$emit("showData", response.data);
          }, 1500);
        })
        .catch((error) => console.error(error))
        .then(() => console.log("hice el get"));
      this.cityInput = "";
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
.search-container {
  width: 80%;
  height: 10%;
  display: flex;
  justify-content: center;
  align-items: center;
  display: flex;
  margin: 0 auto;
  gap: $flexGap;

  input[type="text"] {
    position: relative;
    padding: 15px 20px 15px 20px;
    width: 70%;
    color: #525252;
    text-transform: $textTransform;
    text-align: left;
    font-family: $fontFamily;
    font-size: 10px;
    font-weight: $regularWeight;
    letter-spacing: $textSpacing;
    border: none;
    border-radius: $roundedBorder;
    background: linear-gradient(to right, #ffffff 0%, #464747 #f9f9f9 100%);
    transition: $transition;
    outline: none;

    &::selection {
      background-color: purple;
      color: white;
    }

    &:hover {
      font-size: 12px;
      transition: $transition;
    }
    /* &:focus{
      border: 3px solid blueviolet;
      transition: all 0.2s ease-in-out 0.5s;
    } */
  }

  button {
    padding: 10px;
    border: none;
    border-radius: $roundedBorder;
    outline: none;
    font: inherit;
    color: inherit;
    background-color: rgba($color: #dfdfdf, $alpha: 0.3);
    font-weight: $thinWeight;
    cursor: pointer;
    transition: $transition;
    &:hover {
      background-color: rgba($color: #dfdfdf, $alpha: 0.6);
      transition: $transition;
    }
  }

  i {
    font-size: 20px;
    position: relative;
    color: white;
    &:active {
      font-size: 18px;
      transition: font-size 0.05s ease-in-out;
    }
  }
}
</style>
