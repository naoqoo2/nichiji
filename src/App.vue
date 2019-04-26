<template>
  <div id="app">
    <input v-model="nichiji" placeholder="Please enter the date">
    <p>{{ moment_nichiji }}</p>
    <DateCard
      v-for="card in cards"
      v-bind:key="card.name"
      v-bind:value="moment_nichiji"
      v-bind:format="card.format"
    ></DateCard>
  </div>
</template>

<script>
import moment from "moment";
import DateCard from "./components/DateCard";
// aa
export default {
  name: "App",
  components: {
    DateCard
  },
  data: function() {
    return {
      nichiji: moment(new Date()).format("MM/DD"),
      cards: [
        { name: "One", format: "MM/DD" },
        { name: "Two", format: "YYYY/MM/DD" },
        { name: "Three", format: "YYYY-MM-DD HH:mm:ss" }
      ]
    };
  },
  computed: {
    moment_nichiji: function() {
      var moment_value = moment(this.nichiji);
      if (!moment_value.isValid()) {
        return '';
      }
      return moment_value;
    }
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
