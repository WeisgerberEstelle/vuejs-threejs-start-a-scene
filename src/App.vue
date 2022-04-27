<template>
  <div id="app">
    <Product :material="material" :colors="colors" />
    <ListColors :colors="colors" @chose-a-color="ChoseAColor"/>
  </div>
</template>

<script>
import Product from "./components/Product";
import ListColors from "./components/ListColors";
import { MeshPhongMaterial } from "three";

const INITIAL_MTL = new MeshPhongMaterial({ color: 0xf1f1f1, shininess: 10 });
export default {
  name: "App",
  data() {
    return {
      material: { childID: "cube", mtl: INITIAL_MTL },
      colors: [
        {
          color: "66533C",
        },
        {
          color: "173A2F",
        },
        {
          color: "153944",
        },
        {
          color: "27548D",
        },
        {
          color: "438AAC",
        },
      ],
    };
  },
  components: {
    Product,
    ListColors,
  },
  methods: {
    ChoseAColor(){
      console.log("coucou");
    }
  }
};
</script>

<style>
*,
*::before,
*::after {
  box-sizing: border-box;
}

body,
html {
  margin: 0;
  padding: 0;
  font-family: "Raleway", sans-serif;
  font-size: 14px;
  color: #444444;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  overflow: hidden;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.controls {
  position: absolute;
  bottom: 0;
  width: 100%;
}

.tray {
  width: 100%;
  height: 50px;
  position: relative;
  overflow-x: hidden;
}

.tray__slide {
  position: absolute;
  display: flex;
  left: 0;
  /*   transform: translateX(-50%);
  animation: wheelin 1s 2s ease-in-out forwards; */
}

.tray__swatch {
  transition: 0.1s ease-in;
  height: 50px;
  min-width: 50px;
  flex: 1;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.3);
  background-size: cover;
  background-position: center;
}

.tray__swatch:nth-child(5n + 5) {
  margin-right: 20px;
}
</style>
