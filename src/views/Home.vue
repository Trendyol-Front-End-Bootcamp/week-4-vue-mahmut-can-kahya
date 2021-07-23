<template>
  <div class="container">
    <img alt="StarWars logo" src="../assets/logo.png" width="25%" />

    <input v-model="searchVal" placeholder="Search starships" />
    <div v-if="loading">
      <img src="../assets/1488.gif" />
    </div>
    <StarShipList :starShipsList="starShips" />
    <div
      class="error"
      v-if="(starShips.length <= 0 || statusCode === 204) && !loading"
    >
      No data available
    </div>
  </div>
</template>

<script>
import StarShipList from "../components/StarShipList";
import axios from "axios";

export default {
  name: "Home",
  components: {
    StarShipList,
  },
  data() {
    return {
      loading: true,
      starShips: [],
      searchVal: "",
      statusCode: 0,
    };
  },
  mounted() {
    this.$nextTick(function() {
      // Code that will run only after the
      // entire view has been rendered
      this.loading = true;
      axios
        .get("https://swapi.dev/api/starships/")
        .then((response) => {
          this.starShips = response.data.results;
          this.statusCode = response.status;
        })
        .then(() => {
          this.loading = false;
        });
    });
  },
  watch: {
    searchVal: function(val) {
      axios
        .get(`https://swapi.dev/api/starships/?search=${val}`)
        .then((response) => {
          this.starShips = response.data.results;
        });
    },
  },
};
</script>

<style scoped>
input {
  border: none;
  width: 300px;
  height: 32px;
  border-radius: 16px;
  margin-bottom: 60px;
  background-color: #ffe300;
  margin-top: 24px;
  padding-left: 12px;
  color: #000000;
}
input:focus {
  outline: none;
  color: #ffe300;
  background-color: #000000;
}
.error {
  color: red;
}
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
