# Sphere3D 3D 球体

<!-- USAGE_FREQUENCY: advanced -->

## 描述

3D 视图中的球体。球体由所有与给定点距离相等的点组成。该给定点称为球心，该给定距离称为半径。可以通过提供球心和球面上一点，或提供球心和半径（数字或函数）来构造球体。如果半径为负值，则取其绝对值。

## JessieCode 语法

```js
// 通过球心和球面上一点创建球体
sphere = view.create('sphere3d', [center, point], {});

// 通过球心和半径创建球体
sphere = view.create('sphere3d', [center, radius], {});

// 带属性创建
sphere = view.create('sphere3d', [center, point], <<
    fillOpacity: 0.8,
    fillColor: 'blue'
>>);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| center | Point3D | 球心（必须是 Point3D） |
| point | Point3D/Number/Function | 球面上一点或半径（数字或函数） |

**参数说明**：
- 球心必须作为 Point3D 提供
- 半径可以作为数字（创建固定半径的球体）或另一个 Point3D 提供
- 如果半径以数字或函数形式提供，则取其绝对值

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `fillColor` | String | '#aaaaaa' | 填充颜色 |
| `fillOpacity` | Number | 0.5 | 填充透明度 (0-1) |
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 1 | 线宽（像素） |
| `visible` | Boolean | true | 是否可见 |

## 示例

### 1. 通过两点创建球体

```js
var view = board.create(
    'view3d',
    [[-6, -3], [8, 8],
    [[0, 3], [0, 3], [0, 3]]],
    {
        xPlaneRear: {fillOpacity: 0.2, gradient: null},
        yPlaneRear: {fillOpacity: 0.2, gradient: null},
        zPlaneRear: {fillOpacity: 0.2, gradient: null}
    }
);

// 两个点
var center = view.create(
    'point3d',
    [1.5, 1.5, 1.5],
    {
        withLabel: false,
        size: 5,
   }
);
var point = view.create(
    'point3d',
    [2, 1.5, 1.5],
    {
        withLabel: false,
        size: 5
   }
);

// 球体
var sphere = view.create(
    'sphere3d',
    [center, point],
    {}
);
```

### 2. 球面上的滑点

```js
var view = board.create(
    'view3d',
    [[-6, -3], [8, 8],
    [[-3, 3], [-3, 3], [-3, 3]]],
    {
        depthOrder: {
            enabled: true
        },
        projection: 'central',
        xPlaneRear: {fillOpacity: 0.2, gradient: null},
        yPlaneRear: {fillOpacity: 0.2, gradient: null},
        zPlaneRear: {fillOpacity: 0.2, gradient: null}
    }
);

// 两个点
var center = view.create('point3d', [0, 0, 0], {withLabel: false, size: 2});
var point = view.create('point3d', [2, 0, 0], {withLabel: false, size: 2});

// 球体
var sphere = view.create('sphere3d', [center, point], {fillOpacity: 0.8});

// 球面上的滑点
var glide = view.create('point3d', [2, 2, 0, sphere], {withLabel: false, color: 'red', size: 4});
var l1 = view.create('line3d', [glide, center], { strokeWidth: 2, dash: 2 });
```

### 3. 设置球体样式

```js
// 创建视图
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]],
    {
        projection: 'central'
    });

// 球心和半径点
var center = view.create('point3d', [0, 0, 0], {size: 3});
var radiusPoint = view.create('point3d', [3, 0, 0], {size: 3});

// 半透明蓝色球体
var sphere = view.create('sphere3d', [center, radiusPoint], {
    fillColor: 'blue',
    fillOpacity: 0.3,
    strokeColor: 'darkblue',
    strokeWidth: 2
});
```

### 4. 动态球体

```js
// 创建滑块控制半径
var slider = board.create('slider', [[-4, 4], [4, 4], [0.5, 1, 5]]);

// 创建视图
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 球心
var center = view.create('point3d', [0, 0, 0], {size: 3});

// 半径点（x 坐标随滑块变化）
var radiusPoint = view.create('point3d', [
    function() { return slider.Value(); },
    0, 0
], {size: 3});

// 动态球体
var sphere = view.create('sphere3d', [center, radiusPoint], {
    fillOpacity: 0.5
});
```

### 5. 固定半径球体

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 球心
var center = view.create('point3d', [1, 1, 1], {size: 4});

// 固定半径为 2 的球体
var sphere = view.create('sphere3d', [center, 2], {
    fillColor: 'green',
    fillOpacity: 0.4
});
```

## 注意事项

1. **球心表示**：球心必须作为 Point3D 对象提供
2. **半径处理**：如果半径为负值，其绝对值会被采用
3. **深度排序**：启用 `depthOrder: { enabled: true }` 可以改善多个 3D 元素的层叠显示效果
4. **滑点**：可以在球面上创建滑点，方法是在创建 Point3D 时将球体作为第四个参数传入
5. **投影类型**：可以使用 `projection: 'central'`（透视投影）或 `projection: 'parallel'`（平行投影）

## 相关元素

- [Point3D](./Point3D.md) - 3D 点
- [Line3D](./Line3D.md) - 3D 直线
- [View3D](./View3D.md) - 3D 视图
- [Curve3D](./Curve3D.md) - 3D 曲线
