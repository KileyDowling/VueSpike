<template>
  <div><p>{{deposit.date}}: ${{deposit.amount}}  <span v-on:click="removeDeposit(deposit)">x</span>
</p>
    </div>
</template>

<script>
export default {
  name: "Deposit",
  props: ["deposit"],
  methods: {
    removeDeposit: function(deposit) {
      this.$emit("delete", deposit);
    }
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
.name {
  color: pink;
  font-style: italic;
}
.progress {
  color: deeppink;
  font-weight: bold;
}
.reverseProgress {
  color: lightslategray;
  font-weight: bold;
}
</style>
