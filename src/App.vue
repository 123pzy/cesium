<script setup>
import { onMounted } from "vue";
import HelloCesium from "./components/HelloCesium.vue";
import * as Cesium from "cesium";
import "./Widgets/widgets.css";

console.log("Cesium.Viewer:", Cesium.Viewer);
window.CESIUM_BASE_URL = "/";
// 设置相机的默认视角
Cesium.Camera.DEFAULT_VIEW_RECTANGLE = Cesium.Rectangle.fromDegrees(
  // 西边的经度
  89.5,
  // 南边的纬度
  20.4,
  // 东边的经度
  110.4,
  // 北边的纬度
  61.2
);

// 设置cesium的Token
Cesium.Ion.defaultAccessToken =
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJlNTdjYWQxNy02MTRmLTQ4MTMtOWNjMC0zNDg2N2M4YWI1YTQiLCJpZCI6MTQ5NjE5LCJpYXQiOjE2ODc4NTY2NDJ9.wQCXDM5G0L5FNVvIDzR5nYe6J5I_zzo8JEn6w7QQ0Is";

onMounted(() => {
  window.viewer = new Cesium.Viewer("cesiumContanier", {
    infoBox: false,
    geocoder: false, // 是否显示搜索框按钮
    homeButton: false, // 是否显示home按钮
    sceneModePicker: false, // 是否显示查看器按钮（3D）
    baseLayerPicker: false, // 是否显示图层切换按钮
    navigationHelpButton: false, // 是否显示帮助按钮
    animation: false, // 是否显示播放动画
    timeline: false, // 是否显示时间轴
    fullscreenButton: false, // 是否显示全屏按钮
    // 设置显示地形
    terrainProvider: Cesium.createWorldTerrain({
      requestVertexNormals: true, // 设置光照效果
      requestWaterMask: true, // 设置水波纹效果
    }),
    sceneMode: Cesium.SceneMode.SCENE3D, // 默认值
    // creditContainer:document.createElement('div')
    vrButton: true,
    scene3DOnly: true, // 节省GPU内存，让只支持3D模式
    // 设置天空盒子
    // skyBox: new Cesium.skyBox({
    //   source: {
    //     positiveX: "",
    //     negativeX: "",
    //     positiveY: "",
    //     negativeY: "",
    //     positiveZ: "",
    //     negativeZ: "",
    //   },
    // }),
  });

  viewer.cesiumWidget.creditContainer.style.display = "none"; // 隐藏logo
  console.log(viewer);

  // 屏幕坐标系转二维笛卡尔坐标系  Cartesian2
  // 地理坐标系转WGS-84 Cartographic
  // 笛卡尔转空间直角坐标系 Cartesian3

  // 角度与弧度的转换
  var radians = Cesium.Math.toRadians(90);
  console.log(radians);
});

</script>

<template>
  <HelloCesium></HelloCesium>
  <div id="cesiumContanier"></div>
</template>

<style>
#cesiumContanier {
  height: 100%;
  width: 100%;
}
</style>
