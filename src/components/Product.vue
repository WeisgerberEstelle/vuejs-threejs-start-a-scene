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
    };
  },
  methods: {
    init() {
      //initialize scene and background
      this.scene = new THREE.Scene();
      this.scene.background = new THREE.Color("pink");

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

      this.camera.position.set(0, 0, 16);
      // END: Adding camera

      // START: Adding controls
      const controls = new OrbitControls(this.camera, this.renderer.domElement);

      //controls.enablePan = false;
      controls.target.set(0, 0, 0);
      controls.addEventListener("change", this.renderScene); // use if there is no animation loop
      // END: Adding controls

      // START: Adding light
      const directionalLight = new THREE.DirectionalLight(0xffffff, 2);
      directionalLight.position.set(0, 1, 0);
      directionalLight.castShadow = true;
      this.scene.add(directionalLight);

      const light = new THREE.PointLight(0xffffcc, 1);
      light.position.set(0, 600, 1000);
      this.scene.add(light);

      const light2 = new THREE.PointLight(0xe6f7ff, 1);
      light2.position.set(1000, 200, 0);
      this.scene.add(light2);

      const light3 = new THREE.PointLight(0xfff2e6, 1);
      light3.position.set(0, 200, -1000);
      this.scene.add(light3);

      const light4 = new THREE.PointLight(0xc4c400, 1);
      light4.position.set(-1000, 600, 1000);
      this.scene.add(light4);
      // END: Adding light

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

      //Add an object
      const groundGeometry = new THREE.BoxGeometry(8, 2, 8);
      const groundMaterial = new THREE.MeshPhongMaterial({ color: 0xfafafa });
      const groundMesh = new THREE.Mesh(groundGeometry, groundMaterial);
      groundMesh.receiveShadow = true;
      groundMesh.position.y = -2;
      this.scene.add(groundMesh);

      this.animate();
    },
    renderScene() {
      this.renderer.render(this.scene, this.camera);
    },
    animate() {
      // NOTE: Window is implied.
      // requestAnimationFrame(this.animate.bind(this));
      window.requestAnimationFrame(this.animate.bind(this));
      this.renderScene();
    },
  },
  mounted() {
    this.init();
  },
};
</script>
