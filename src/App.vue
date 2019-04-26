<template>
  <div id="app">
    <input v-model="nichiji" placeholder="Please enter the date">
    <p>{{ moment_nichiji }}</p>
    <div v-if="moment_nichiji">
      <DateCard
        v-for="card in cards"
        v-bind:key="card.name"
        v-bind:value="format_nichiji(card.format.type, card.format.value)"
      ></DateCard>
    </div>
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
      nichiji: moment(new Date()).format("YYYY/MM/DD"),
      cards: [
        { name: "1", format: {type: "moment", value:"MM/DD"}},
        { name: "2", format: {type: "moment", value:"seireki"}},
        { name: "3", format: {type: "date", value:"wareki"}},
        { name: "4", format: {type: "moment", value:"YYYY-MM-DD HH:mm:ss"}}
      ]
    };
  },
  computed: {
    moment_nichiji: function() {
      var moment_value = moment(this.nichiji);
      if (!moment_value.isValid()) {
        return false;
      }
      return moment_value;
    },
    date_nichiji: function() {
      return new Date(this.moment_nichiji);
    }
  },
  methods: {
    format_nichiji: function(type, format) {
      if (type === "moment") {
        if (typeof format_functions[format] == "function") {
          return format_functions[format](this.moment_nichiji);
        } else {
          return this.moment_nichiji.format(format);
        }
      } else if (type === "date") {
        if (typeof format_functions[format] == "function") {
          return format_functions[format](this.date_nichiji);
        } else {
          return this.date_nichiji;
        }
      }
    }
  }
};
var format_functions = {
  seireki: function(moment_nichiji) {
    return "西暦" + moment_nichiji.format("YYYY");
  },
  wareki: function(date_nichiji) {
    return date_nichiji.toLocaleDateString('ja-JP-u-ca-japanese', {
      era    : 'long',  // 時代 : 'narrow' にすると '平成' は 'H' になる
      year   : 'numeric',  // 年 : 'ja-JP-u-ca-japanese' の場合は和暦
      month  : 'long',  // 月
      day    : 'numeric',  // 日
      weekday: 'short',  // 曜日 : 'long' で '金曜日'・'short' で '(金)' になる
      hour12 : true,  // 時間の12時間表記 : true にすると '16' (時) ではなく '午後4' (時) になる
      hour   : 'numeric',  // 時
      minute : 'numeric',  // 分
      second : 'numeric'   // 秒
    });
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
