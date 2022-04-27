<template>
  <div id="app">
    <Product :material="material" />
  </div>
</template>

<script>
import Product from "./components/Product";
import { MeshPhongMaterial } from "three";

const INITIAL_MTL = new MeshPhongMaterial({ color: 0xf1f1f1, shininess: 10 });
export default {
  name: "App",
  data() {
    return {
      material: { childID: "cube", mtl: INITIAL_MTL },
    };
  },
  components: {
    Product,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
