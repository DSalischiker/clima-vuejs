<template>
  <div id="app">
    <Weather/>
  </div>
</template>

<script>
import Weather from '@/components/Weather.vue';
export default {
  name: "App",
  components: {
    Weather,
  },
};
</script>

<style lang="scss">
body{
background: #252525;
width: 100%;
height: 100vh;
margin: 0;
padding: 0;
::selection{
  background-color:white;
  color: #252525;
  }
}
#app {
  font-family: $fontFamily;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  height: 100vh;
  display: flex;
  align-items: center;
}
</style>
