<template>
  <div class="main-container">
    <SceneViewer v-if="isMap" ref="map" @ready="ready" />
    <Left />
    <div class="set">
      <button @click="setSun">setSun</button>
      <button @click="sethomeCamera">sethomeCamera</button>
    </div>
    <Right />
  </div>
</template>
<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import Left from '../components/Left.vue';
import Right from '../components/Right.vue';
import SceneViewer from '../components/SceneViewer.vue';
import { ref } from 'vue';
// 引用cesium
import 'cesium/Build/Cesium/Widgets/widgets.css';
import * as Cesium from 'cesium/Build/Cesium';

const isMap = ref(true);
let viewer = null;
const ready = viewer2 => {
  // eslint-disable-next-line no-console
  console.log('ready');
  // eslint-disable-next-line no-console
  console.log(viewer2);
  viewer = viewer2;
};
const setSun = () => {
  // Enable lighting based on the sun position
  viewer.scene.globe.enableLighting = true;
};
const sethomeCamera = () => {
  // Create an initial camera view
  var initialPosition = new Cesium.Cartesian3.fromDegrees(
    -73.998114468289017509,
    40.674512895646692812,
    2631.082799425431,
  );
  var initialOrientation = new Cesium.HeadingPitchRoll.fromDegrees(
    7.1077496389876024807,
    -31.987223091598949054,
    0.025883251314954971306,
  );
  var homeCameraView = {
    destination: initialPosition,
    orientation: {
      heading: initialOrientation.heading,
      pitch: initialOrientation.pitch,
      roll: initialOrientation.roll,
    },
  };
  // Set the initial view
  viewer.scene.camera.setView(homeCameraView);
};
</script>

<style lang="scss" scoped>
.main-container {
  height: 100%;
  overflow: hidden;
  position: relative;
}
.set {
  position: absolute;
  top: 0;
  right: 50%;
  z-index: 999;
  button {
    margin: 10px;
  }
}
</style>
