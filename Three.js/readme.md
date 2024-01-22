# three.js

## 坑点
版本更新变化：
- 注意 `three.js` 的版本，新版本`THREE.AxisHelper`已经弃用，现在用的是`THREE.AxesHelper` 👉[文档](https://threejs.org/docs/#api/zh/helpers/AxesHelper)
- `renderer.shadowMapEnabled`,现在已经改为`renderer.shadowMap.enable`

其他：
- 注意`planeGeometry`的参数width 是沿着x 轴的，height 是沿着y轴的