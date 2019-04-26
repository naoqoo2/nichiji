<template>
  <div id="app">
    <input v-model="nichiji" placeholder="Please enter the date">
    <DateCard
      v-for="card in cards"
      v-bind:key="card.name"
      v-bind:value="nichiji"
      v-bind:format="card.format"
    ></DateCard>
  </div>
</template>

<script>
import DateCard from "./components/DateCard";
// aa
export default {
  name: "App",
  components: {
    DateCard
  },
  data: function() {
    return {
      nichiji: "",
      cards: [
        { name: "One", format: "A" },
        { name: "Two", format: "B" },
        { name: "Three", format: "C" }
      ]
    };
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
