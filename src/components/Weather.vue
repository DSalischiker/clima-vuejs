<template>
  <div>
    <h1>Clima</h1>
    <Search />
    <Data />
  </div>
</template>

<script>
import Search from "@/components/Search.vue";
import Data from "@/components/Data.vue";
export default {
  name: "Clima",
  components: {
    Search,
    Data,
  },
};
</script>

<style lang="scss" scoped></style>
