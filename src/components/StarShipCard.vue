<template>
  <div class="card" @click="clickedCard">
    <div class="image-wrapper">
      <img src="../assets/starship.jpeg" />
      <div class="rating">
        <span>{{ starship.hyperdrive_rating }}</span>
      </div>
    </div>
    <h2>{{ starship.name }}</h2>
    <h3>{{ starship.model }}</h3>
  </div>
</template>

<script>
import { router } from "../router/index";

export default {
  name: "StarShipCard",
  props: {
    starship: {
      name: {
        type: String,
        default: "Starship Name",
      },
      model: {
        type: String,
        default: "Starship Model",
      },
      hyperdrive_rating: {
        type: Number,
        default: "Hyperdrive Rating",
      },
    },
  },
  mounted() {
    this.$nextTick(function() {
      // Code that will run only after the
      // entire view has been rendered
    });
  },
  methods: {
    clickedCard: function() {
      let detailId = this.starship.url.split("/").reverse()[1];
      router.push({
        path: `/detail/${detailId}`,
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h2 {
  color: black;
  font-size: 24px;
  font-weight: 800;
}
h3 {
  color: grey;
  font-size: 18px;
  font-weight: 500;
}
.card {
  position: relative;
  display: flex;
  flex: 1;
  width: 300px;
  flex-direction: column;
}
.card:hover {
  transform: scale(1.22);
}
.image-wrapper > img {
  width: 200px;
}
.rating {
  position: absolute;
  top: 0;
  right: 0;
  background-color: lightgreen;
  border-radius: 70%;
  padding: 8px;
}
</style>
