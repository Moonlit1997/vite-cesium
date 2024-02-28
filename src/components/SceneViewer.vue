<template>
  <div id="sceneViewer" class="scene-viewer"></div>
</template>

<script setup>
import { onMounted } from 'vue';

// 引用cesium
import 'cesium/Build/Cesium/Widgets/widgets.css';
import * as Cesium from 'cesium/Build/Cesium';

onMounted(() => {
  // 设置cesium的token
  Cesium.Ion.defaultAccessToken = window.defaultAccessToken;
  // eslint-disable-next-line no-unused-vars
  const viewer = new Cesium.Viewer('sceneViewer', {
    animation: true, // 动画小组件
    baseLayerPicker: false, // 底图组件，选择三维数字地球的底图（imagery and terrain）。
    fullscreenButton: false, // 全屏组件
    vrButton: false, // VR模式
    geocoder: false, // 地理编码（搜索）组件
    homeButton: false, // 首页，点击之后将视图跳转到默认视角
    infoBox: false, // 信息框
    sceneModePicker: true, // 场景模式，切换2D、3D 和 Columbus View (CV) 模式。
    selectionIndicator: false, // 是否显示选取指示器组件
    timeline: true, // 时间轴
    navigationHelpButton: false, // 帮助提示，如何操作数字地球。
    // 如果最初应该看到导航说明，则为true；如果直到用户明确单击该按钮，则该提示不显示，否则为false。
    navigationInstructionsInitiallyVisible: false,
  });

  // Enable lighting based on the sun position
  viewer.scene.globe.enableLighting = true;

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
});
</script>

<style scoped lang="scss">
.scene-viewer {
  height: 100%;
}
</style>
