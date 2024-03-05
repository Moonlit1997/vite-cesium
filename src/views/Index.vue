<template>
  <div class="main-container">
    <SceneViewer v-if="isMap" ref="map" @ready="ready" />
    <Left />
    <div class="set">
      <button @click="setSun">setSun</button>
      <button @click="sethomeCamera">sethomeCamera</button>
      <button @click="setEntity">setEntity</button>
      <button @click="settwoPoint">settwoPoint</button>
      <button @click="clear">clear</button>
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
const setEntity = () => {
  viewer.entities.add({
    name: 'BBox',
    position: Cesium.Cartesian3.fromDegrees(120.55538, 31.87532, 100.0),
    box: {
      dimensions: new Cesium.Cartesian3(40.0, 100.0, 150.0),
      material: Cesium.Color.BLUE,
    },
  });
  viewer.zoomTo(viewer.entities);
};
const settwoPoint = () => {
  viewer.entities.add({
    name: 'Red line on the surface',
    polyline: {
      positions: Cesium.Cartesian3.fromDegreesArrayHeights([120.55538, 31.87532, 0, 120.55538, 31.87532, 1000]),
      width: 5,
      material: new Cesium.PolylineOutlineMaterialProperty({
        color: Cesium.Color.RED,
      }),
    },
  });
  viewer.zoomTo(viewer.entities);
};
const clear = () => {
  viewer.entities.removeAll();
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
