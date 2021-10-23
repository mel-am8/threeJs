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
  scene = new THREE.Scene();
  camera = new THREE.PerspectiveCamera(
    45,
    window.innerWidth / window.innerHeight,
    0.1,
    1000
  );
  renderer = new THREE.WebGLRenderer({
    canvas: document.querySelector("#myCanvas") as Canvas,
  });
  axes = new THREE.AxesHelper(20);

  cubeGeo = new THREE.BoxGeometry(4, 4, 4);
  cubeMat = new THREE.MeshBasicMaterial({
    color: 0xff0000,
    wireframe: true,
  });
  cube = new THREE.Mesh(this.cubeGeo, this.cubeMat);

  mounted(): void {
    this.renderer.setClearColor(new THREE.Color(0xeeeeee));
    this.renderer.setSize(window.innerWidth, window.innerHeight);
    this.scene.add(this.axes);
    this.scene.add(this.cube);
    this.renderer.render(this.scene, this.camera);
  }
}
</script>
