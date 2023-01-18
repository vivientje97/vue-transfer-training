<template>
  <div id="app">
    <DualSelects
      leftLabel="Source"
      rightLabel="Target"
      :leftData="leftData"
      :rightData="rightData"
    ></DualSelects>
    <!-- <p>
      debug: leftUsers, {{ leftData }}
      <br>
      rightUsers, {{ rightData }}
    </p> -->
  </div>
</template>

<script>
import DualSelects from "./components/DualSelects";

export default {
  name: "App",
  components: {
    DualSelects
  },
  data() {
    return {
      leftData: [
        "Campina",
        "Douwe Egberts",
        "Coca-Cola",
        "Heineken",
        "Unox",
        "Dr Oetker",
        "Amstel",
        "Glorix",
        "Knorr",
        "Calvè"
      ],
      rightData: [],
      
    };
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
