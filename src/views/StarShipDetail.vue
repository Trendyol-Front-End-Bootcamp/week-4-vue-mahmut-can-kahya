<template>
  <div class="detail">
    <div class="back-arrow" @click="backButton">
      <img src="../assets/back-arrow.svg" />
      <p>Back to Starship List</p>
    </div>
    <div v-if="loading">
      <img src="../assets/1488.gif" />
    </div>
    <div v-else class="detail-wrapper">
      <img src="../assets/starship.jpeg" />
      <h1>{{ starship.name }}</h1>
      <span>{{ starship.hyperdrive_rating }}</span>
      <div class="row" v-for="(detail, index) in detailList" :key="index">
        <span>{{ detail.text }} </span>
        <h4>{{ starship[detail.key] }}</h4>
      </div>
    </div>
  </div>
</template>

<script>
import { router } from "../router/index";
import axios from "axios";
export default {
  name: "StarShipDetail",
  data() {
    return {
      starship: {},
      detailList: [
        { key: "model", text: "Model:" },
        { key: "passengers", text: "Passengers:" },
        { key: "max_atmosphering_speed", text: "Max Atmosphering Speed:" },
        { key: "manufacturer", text: "Manufacturer: " },
        { key: "crew", text: "Crew: " },
        { key: "cargo_capacity", text: "Cargo Capacity: " },
      ],
      loading: true,
    };
  },
  mounted() {
    this.$nextTick(function() {
      // Code that will run only after the
      // entire view has been rendered
      let id = this.$route.params.id;
      this.loading = true;
      axios
        .get(`https://swapi.dev/api/starships/${id}/`)
        .then((response) => {
          this.starship = response.data;
        })
        .then(() => {
          this.loading = false;
        });
    });
  },
  methods: {
    backButton: function() {
      router.push({
        path: `/`,
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.detail {
  display: flex;
  flex-direction: row;
  justify-content: center;
  position: relative;
}
.detail > .back-arrow {
  position: absolute;
  display: flex;
  flex-direction: row;
  top: 0;
  left: 50px;
}
.back-arrow > img {
  width: 50px;
}
.back-arrow > p {
  font-size: 18px;
  font-weight: 700;
}
.detail-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border: solid 1px grey;
  padding: 20px;
  background-color: yellow;
  border-radius: 28px;
  position: relative;
}
.detail-wrapper > img {
  width: 300px;
  margin-bottom: 20px;
}
.detail-wrapper > span {
  position: absolute;
  top: 0;
  right: 3px;
  border: 1px solid grey;
  border-radius: 28px;
  padding: 5px;
}
h4 {
  font-size: 18px;
  font-weight: 600;
  margin-left: 3px;
  padding-top: 3px;
}
span {
  font-size: 20px;
  color: black;
  font-weight: 500;
}
.row {
  display: flex;
  flex-direction: row;
  align-items: center;
  height: 45px;
}
</style>
