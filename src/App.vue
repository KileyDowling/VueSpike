<template>
  <div id="app">
  <!--  <HelloLovely msg="Hello, Lovely" goal=100 previousProgress=25 addedValue=0 latest=0 getLatest=0 /> -->
   <HelloLovely /> 
  </div>
</template>

<script>
import HelloLovely from "./components/HelloLovely.vue";

export default {
  name: "app",
  components: {
    HelloLovely
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
