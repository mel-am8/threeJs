<template>
  <v-container>
    <canvas id="myCanvas"></canvas>
  </v-container>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import * as THREE from "three";

export type Canvas = HTMLCanvasElement;

@Component({
  components: {
    Sample,
  },
})
export default class Sample extends Vue {
  mounted(): void {
    let scene = new THREE.Scene();

    let camera = new THREE.PerspectiveCamera(
      60,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );

    camera.position.x = -30;
    camera.position.y = 40;
    camera.position.z = 30;
    camera.lookAt(scene.position);

    let axes = new THREE.AxesHelper(20);

    let cubeGeo = new THREE.BoxGeometry(4, 4, 4);
    let cubeMat = new THREE.MeshBasicMaterial({
      color: 0xff0000,
      wireframe: true,
    });
    let cube = new THREE.Mesh(cubeGeo, cubeMat);

    cube.position.x = -4;
    cube.position.y = 3;
    cube.position.z = 0;

    let renderer = new THREE.WebGLRenderer({
      canvas: document.querySelector("#myCanvas") as Canvas,
    });

    renderer.setClearColor(new THREE.Color(0xeeeeee));
    renderer.setSize(window.innerWidth, window.innerHeight);
    scene.add(axes);
    scene.add(cube);

    renderer.render(scene, camera);

  }
}
</script>
