<template>
  <div id="app">
    <div class="row p-0 m-2">
      <div class="card col">
        <div class="card-header bg-secondary text-light">Tiempos de uso</div>

        <pc-component v-for="pc in maquinas" :pc="pc" :key="pc.name">
        </pc-component>
      </div>
      <div class="card col">
        <div class="card-header bg-secondary text-light">Impresiones</div>
      </div>
    </div>
  </div>
</template>

<script>
// var moment = require("moment");
import PcComponent from "./components/pc-component.vue";

export default {
  name: "App",
  components: {
    PcComponent
  },
  data: function() {
    return {
      maquinas: {
        pc1: {
          name: "PC1",
          docs: {}
        },
        pc2: {
          name: "PC2",
          docs: {}
        },
        pc3: {
          name: "PC3",
          docs: {}
        },
        pc4: {
          name: "PC4",
          docs: {}
        },
        pc5: {
          name: "PC5",
          docs: {}
        },
        pc6: {
          name: "PC6",
          docs: {}
        },
        pc7: {
          name: "PC7",
          docs: {}
        },
        pc8: {
          name: "PC8",
          docs: {}
        }
      },
      impresiones: {}
    };
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
