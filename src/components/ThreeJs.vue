<template>
  <div class="divCenter pt-20">
    <!-- <div id="loading" class="divCenter w-full mt-[15rem] animate-spin"></div> -->
    <div
      id="threejs-container"
      class=""
      :style="
        windowWidth < 1280
          ? null
          : {
              'padding-left': paddingValue - 50 + 'px',
              'padding-right': paddingValue - 50 + 'px'
            }
      "
    />
  </div>
</template>

<script>
/* eslint-disable */
  import * as THREE from 'three';
  import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls';
  import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';
  import { RoomEnvironment } from 'three/examples/jsm/environments/RoomEnvironment.js';

  /* eslint-enable */
export default {
	props: {
		paddingValue: {
			type: Number,
			default: 0
		}
	},
	data() {
		return {
			hasUnintendedBehaviors: false
		};
	},
	mounted() {
		let isInDesktop = window.innerWidth > 1148;
		const userPlatform = (platform) => {
			return platform ? 5 : 3;
		};

		const camera = new THREE.PerspectiveCamera(75, 2, 0.1, 1000);
		camera.position.x = 30;
		camera.position.y = 20;
		camera.position.z = 30;

		const loader = new GLTFLoader();
		loader.load(
			' ./web/source/laptop.glb',
			function (gltf) {
				const model = gltf.scene;

				// position the model from the camera
				model.position.set(0, 0, 6);
				model.scale.set(
					userPlatform(isInDesktop),
					userPlatform(isInDesktop),
					userPlatform(isInDesktop)
				); //model size
				model.castShadow = true;
				scene.add(model);
			},
			undefined,
			function (error) {
				this.$router.push('notfound');
			}
		);

		const container = document.getElementById('threejs-container');

		// three js renderer and size on the element
		const renderer = new THREE.WebGLRenderer(
			{ antialias: true },
			{ alpha: true }
		);
		renderer.setPixelRatio(window.devicePixelRatio);
		renderer.outputEncoding = THREE.sRGBEncoding;
		renderer.setSize(450, 450 / 2); // size
		renderer.shadowMap.enabled = true;
		renderer.shadowMap.type = THREE.PCFSoftShadowMap;
		container.appendChild(renderer.domElement);
		renderer.setClearColor(0x000000, 0); // set transparent bg

		// attempt to add sadows
		const pmremGenerator = new THREE.PMREMGenerator(renderer);

		const scene = new THREE.Scene();
		// scene.background = new THREE.Color( 0xbfe3dd );
		scene.environment = pmremGenerator.fromScene(
			new RoomEnvironment(),
			1
		).texture;

		// lightning and casting shadows
		const light = new THREE.DirectionalLight(0x404040, 1); // soft white light
		light.position.set(15, 20, 0);
		light.target.position.set(0, 0, 0);
		light.castShadow = true;

		light.shadow.mapSize.width = 512; // default
		light.shadow.mapSize.height = 512; // default
		scene.add(light);
		scene.add(light.target);

		// helpers
		const controls = new OrbitControls(camera, renderer.domElement); // allow users to view around the model
		controls.enableDamping = true; // adds a physic effect of "inertia" when spinning camera
		controls.maxPolarAngle = Math.PI / 2 - 0.3; // don't let user view below the ground, 0.3 is slightly above the base level
		controls.minDistance = 10; // don't let user zoom too close
		controls.maxDistance = 50; // don't let user zoom too far away

		controls.enableRotate = true;
		controls.rotateSpeed = 0.3; // set rotation speed of the mouse

		controls.autoRotate = true; // auto rotate
		controls.autoRotateSpeed = 1.5; // 30 seconds per orbit when fps is 60

		// grid helper
		const gridHelper = new THREE.GridHelper(200, 50); // add a grid
		// light helper
		const helper = new THREE.DirectionalLightHelper(light, 5);

		const animate = () => {
			requestAnimationFrame(animate);

			const width = window.innerWidth / 2;
			const height = window.innerHeight / 2;
			camera.aspect = window.innerWidth / window.innerHeight;
			camera.updateProjectionMatrix();
			renderer.setSize(width, height);

			controls.update();
			renderer.render(scene, camera);
		};
		animate();
	}
};
</script>

<style scoped>
  #threejs-container {
    width: 100%;
    height: 50%;
    display: flex;
    justify-content: center;
    text-align: center;
  }

  #threejs-container > canvas {
    display: inline;
  }

  #loading {
    border: 10px solid #f3f3f3; /* Light grey */
    border-top: 10px solid var(--text); /* Blue */
    border-radius: 50%;
    width: 80px;
    height: 80px;
    animation: spin 1s linear infinite;
  }
</style>
