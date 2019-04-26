<template>
  <div class="hello">
    <h2>{{ format }}</h2>
    <h2>{{ value }}</h2>
  </div>
</template>

<script>
export default {
  name: "DateCard",
  props: {
    format: String,
    value: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
