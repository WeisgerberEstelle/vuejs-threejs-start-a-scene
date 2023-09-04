<template>
  <div>
    <div id="myThreeJsCanvas"></div>
    <ListColors :colors="colors" @color-click="ChoseAColor($event)" />
  </div>
</template>
<script>
import * as THREE from "three";
import ListColors from "./ListColors";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";
//import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader";

export default {
  name: "ProductView",
  data() {
    return {
      scene: undefined,
      camera: undefined,
      renderer: undefined,
      controls: undefined,
      groundMaterial: undefined,
      groundMesh: undefined,
    };
  },
  components: {
    ListColors,
  },
  props: {
    material: Object,
    colors: Array,
  },

  methods: {
    init() {
      const BACKGROUND_COLOR = "pink";
      //initialize scene and background
      this.scene = new THREE.Scene();
      this.scene.background = new THREE.Color(BACKGROUND_COLOR);

      //initialize renderer
      this.renderer = new THREE.WebGLRenderer({
        container,
        antialias: true,
        alpha: true,
      });
      this.renderer.setPixelRatio(window.devicePixelRatio);
      this.renderer.outputEncoding = THREE.sRGBEncoding;

      //get container
      const container = document.getElementById("myThreeJsCanvas");
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      this.renderer.shadowMap.enabled = true;
      container.appendChild(this.renderer.domElement);

      // START: Adding camera
      this.camera = new THREE.PerspectiveCamera(
        45,
        container.offsetWidth / container.offsetHeight,
        1,
        1000
      );

      //Floor : Adding floor
      const floorGeometry = new THREE.PlaneGeometry(5000, 5000, 1, 1);
      const floorMaterial = new THREE.MeshPhongMaterial({
        color: "lightblue",
        shininess: 0,
      });

      var floor = new THREE.Mesh(floorGeometry, floorMaterial);
      floor.rotation.x = -0.5 * Math.PI;
      floor.receiveShadow = true;
      floor.position.y = -4;
      this.scene.add(floor);

      this.camera.position.set(0, 3, 16);
      // END: Adding camera

      // START: Adding controls
      this.controls = new OrbitControls(this.camera, this.renderer.domElement);
      this.controls.autoRotate = false;
      this.controls.enablePan = false;
      this.controls.enableDamping = true;
      this.controls.target.set(0, 0, 0);
      this.controls.addEventListener("change", this.renderScene); // use if there is no animation loop
      window.addEventListener("resize", () => this.onWindowResize(), false);
      // END: Adding controls

      // START: Adding light
      const directionalLight = new THREE.DirectionalLight(0xffffff, 0.5);
      directionalLight.position.set(3, 3, 0);
      directionalLight.castShadow = true;
      this.scene.add(directionalLight);

      // const light = new THREE.PointLight(0xffffcc, 0.5);
      // light.position.set(0, 600, 1000);
      // this.scene.add(light);

      const light2 = new THREE.PointLight(0xe6f7ff, 0.5);
      light2.position.set(1000, 200, 0);
      this.scene.add(light2);

      const light3 = new THREE.PointLight(0xfff2e6, 0.5);
      light3.position.set(0, 200, -1000);
      this.scene.add(light3);

      const light4 = new THREE.PointLight(0xc4c400, 0.5);
      light4.position.set(-1000, 600, 1000);
      this.scene.add(light4);

      const hemiLight = new THREE.HemisphereLight(0xffffff, 0xffffff, 0.2);
      hemiLight.position.set(0, 50, 0);
      // Ajoute une lumière hémisphérique à la scène
      this.scene.add(hemiLight);
      // END: Adding light

      // START: Adding gtlf model
      // let loader = new GLTFLoader();

      // loader.load(
      //   "https://s3-us-west-2.amazonaws.com/s.cdpn.io/1376484/chair.glb",
      //  function( data) {
      //     var object = data.scene;
      //     object.position.set(0,0,0);
      //     this.scene.add(object);
      //   }
      // );
      // END: Adding gtlf model
      //texture loader

      // const loader = new THREE.TextureLoader();
      // const logo = loader.load("../assets/logo.png")
      // console.log(logo);
      //Add an object
      const groundGeometry = new THREE.BoxGeometry(8, 2, 8);
      // this.groundMaterial = new THREE.MeshPhongMaterial({
      //   color: "pink",
      //   shininess: 5,
      // });

      var loader = new THREE.TextureLoader();
      this.groundMaterial = [
        "https://cdn.pixabay.com/photo/2018/04/22/12/16/pattern-3340885_960_720.png",
        "https://cdn.pixabay.com/photo/2022/04/10/01/40/background-7122533_960_720.jpg",
        "https://cdn.pixabay.com/photo/2021/09/04/13/47/flowers-6597862_960_720.png",
        "https://cdn.pixabay.com/photo/2018/04/22/12/25/flowers-3340913_960_720.png",
        "https://cdn.pixabay.com/photo/2017/08/30/13/23/mesh-2697072_960_720.png",
        "https://cdn.pixabay.com/photo/2016/03/06/16/23/background-1240686_960_720.png",
      ].map((pic) => {
        return new THREE.MeshLambertMaterial({ map: loader.load(pic) });
      });

      this.groundMesh = new THREE.Mesh(groundGeometry, this.groundMaterial);
      this.groundMesh.receiveShadow = true;
      this.groundMesh.castShadow = true;
      this.groundMesh.position.set(0, -2, -3);
      this.groundMesh.nameID = this.material.childID;

      this.scene.add(this.groundMesh);

      this.animate();
    },

    // render scene
    renderScene() {
      this.renderer.render(this.scene, this.camera);
    },

    //loop animation
    animate() {
      // NOTE: Window is implied.
      // requestAnimationFrame(this.animate.bind(this));
      window.requestAnimationFrame(this.animate.bind(this));
      this.renderScene();
      this.controls.update();
    },
    // if window is resized
    onWindowResize() {
      this.camera.aspect = window.innerWidth / window.innerHeight;
      this.camera.updateProjectionMatrix();
      this.renderer.setSize(window.innerWidth, window.innerHeight);
    },
    ChoseAColor(e) {
      let color = this.colors[parseInt(e.target.dataset.key)];

      if (color.texture) {
        let texture = new THREE.TextureLoader().load(color.texture);
        texture.repeat.set(color.size[0], color.size[1], color.size[2]);
        texture.wrapS = THREE.RepeatWrapping;
        texture.wrapT = THREE.RepeatWrapping;
        this.groundMaterial = new THREE.MeshPhongMaterial({
          map: texture,
          shininess: color.shininess ? color.shininess : 10,
        });
      } else {
        this.groundMaterial = new THREE.MeshPhongMaterial({
          color: "#" + color.color,
          shininess: color.shininess ? color.shininess : 10,
        });
      }
      this.groundMesh.material = this.groundMaterial;
    },
  },

  mounted() {
    this.init();
  },
};
</script>
