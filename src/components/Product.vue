<template>
  <div id="myThreeJsCanvas"></div>
</template>
<script>
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";
export default {
  name: "ProductView",
  data() {
    return {
      scene: undefined,
      camera: undefined,
      renderer: undefined,
      controls: undefined,
      groundMaterial: undefined,
      image: "../assets/logo.png",
    };
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
      const swatches = document.querySelectorAll(".tray__swatch");
      console.log(swatches)
      for (const swatch of swatches) {
        swatch.addEventListener("click", () => console.log("hy"));
      }
      // START: Adding gtlf model
      //   let loader = new GLTFLoader();
      //   loader.load(
      //     this.modelSettings.link,
      //     data => {
      //       var object = data.scene;
      //       object.position.set(0,0,0);
      //       if(this.modelSettings.scale) object.scale.set(this.modelSettings.scale, this.modelSettings.scale, this.modelSettings.scale);
      //       this.scene.add(object);
      //       this.renderScene();
      //     }
      //   );
      // END: Adding gtlf model
      //texture loader

      // const loader = new THREE.TextureLoader();
      // const logo = loader.load("../assets/logo.png")
      // console.log(logo);
      //Add an object
      const groundGeometry = new THREE.BoxGeometry(8, 2, 8);
      this.groundMaterial = this.material.mtl;
      const groundMesh = new THREE.Mesh(groundGeometry, this.groundMaterial);
      groundMesh.receiveShadow = true;
      groundMesh.castShadow = true;
      groundMesh.position.set(0, -2, -3);
      groundMesh.nameID = this.material.childID;

      this.scene.add(groundMesh);

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
    // if wi
    onWindowResize() {
      this.camera.aspect = window.innerWidth / window.innerHeight;
      this.camera.updateProjectionMatrix();
      this.renderer.setSize(window.innerWidth, window.innerHeight);
    },

    setMaterial(material) {
      this.groundMaterial = material;
    },

    selectSwatch() {
      // let color = this.colors[parseInt(e.target.dataset.key)];
      // let new_mtl;

      // new_mtl = new THREE.MeshPhongMaterial({
      //   color: parseInt("0x" + color.color),
      //   shininess: color.shininess ? color.shininess : 10,
      // });

      // this.setMaterial(new_mtl);
      console.log("hey")
    },
  },
  mounted() {
    this.init();
  },
};
</script>
