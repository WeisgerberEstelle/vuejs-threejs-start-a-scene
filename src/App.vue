<template>
  <div id="app">
    <Product :material="material" :colors="colors" />
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
      colors: [
        {
          color: "131417",
        },
        {
          color: "374047",
        },
        {
          color: "5f6e78",
        },
        {
          color: "7f8a93",
        },
        {
          color: "97a1a7",
        },
        {
          color: "acb4b9",
        },
        {
          color: "DF9998",
        },
        {
          color: "7C6862",
        },
        {
          color: "A3AB84",
        },
        {
          color: "D6CCB1",
        },
        {
          color: "F8D5C4",
        },
        {
          color: "A3AE99",
        },
        {
          color: "EFF2F2",
        },
        {
          color: "B0C5C1",
        },
        {
          color: "8B8C8C",
        },
        {
          color: "565F59",
        },
        {
          color: "CB304A",
        },
        {
          color: "FED7C8",
        },
        {
          color: "C7BDBD",
        },
        {
          color: "3DCBBE",
        },
        {
          color: "264B4F",
        },
        {
          color: "389389",
        },
        {
          color: "85BEAE",
        },
        {
          color: "F2DABA",
        },
        {
          color: "F2A97F",
        },
        {
          color: "D85F52",
        },
        {
          color: "D92E37",
        },
        {
          color: "FC9736",
        },
        {
          color: "F7BD69",
        },
        {
          color: "A4D09C",
        },
        {
          color: "4C8A67",
        },
        {
          color: "25608A",
        },
        {
          color: "75C8C6",
        },
        {
          color: "F5E4B7",
        },
        {
          color: "E69041",
        },
        {
          color: "E56013",
        },
        {
          color: "11101D",
        },
        {
          color: "630609",
        },
        {
          color: "C9240E",
        },
        {
          color: "EC4B17",
        },
        {
          color: "281A1C",
        },
        {
          color: "4F556F",
        },
        {
          color: "64739B",
        },
        {
          color: "CDBAC7",
        },
        {
          color: "946F43",
        },
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
        {
          texture:
            "https://cdn.pixabay.com/photo/2018/04/22/12/25/flowers-3340913_960_720.png",
          size: [2, 2, 2],
          shininess: 60,
        },
        {
          texture:
            "https://cdn.pixabay.com/photo/2018/04/06/15/17/pattern-3296033_960_720.png",
          size: [3, 3, 3],
          shininess: 0,
        },
      ],
    };
  },
  components: {
    Product,
  },
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
