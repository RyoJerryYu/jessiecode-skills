# Axes3D 3D 坐标轴

## 描述

一个容器元素，用于创建 3D 视图的坐标轴以及前后平面。

*定义于：* [box3d.js](./src/src_3d_box3d.js.md)

## JessieCode 语法

```js
// 创建 3D 视图和坐标轴
view = view3d(
    [[xMin, yMin], [xMax, yMax]],
    [[xBoundMin, xBoundMax], [yBoundMin, yBoundMax], [zBoundMin, zBoundMax]]
) <<
    axesPosition: 'border',  // 或 'center'
    withAxes3d: true
>>;

// 或显式创建 axes3d 元素
axes = axes3d() <<
    axesPosition: 'center',
    withLabel: true
>>;
```

## 参数

### 方式一：边框坐标轴 (`axesPosition: 'border'`)

| 参数 | 类型 | 描述 |
|------|------|------|
| `axesPosition` | String | `'border'` - 坐标轴显示在视图边框 |

### 方式二：中心坐标轴 (`axesPosition: 'center'`)

| 参数 | 类型 | 描述 |
|------|------|------|
| `axesPosition` | String | `'center'` - 坐标轴从原点 (0,0,0) 显示 |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `axesPosition` | String | `'border'` | 坐标轴位置：`'border'` 或 `'center'` |
| `withAxes3d` | Boolean | true | 是否显示 3D 坐标轴 |
| `withLabel` | Boolean | false | 是否显示轴标签 |
| `strokeColor` | String | '#000000' | 坐标轴颜色 |
| `strokeWidth` | Number | 2 | 坐标轴线宽 |
| `xPlaneRear` | Object | - | 后侧 x 平面属性 |
| `yPlaneRear` | Object | - | 后侧 y 平面属性 |
| `zPlaneRear` | Object | - | 后侧 z 平面属性 |
| `xPlaneFront` | Object | - | 前侧 x 平面属性 |
| `yPlaneFront` | Object | - | 前侧 y 平面属性 |
| `zPlaneFront` | Object | - | 前侧 z 平面属性 |

### 平面属性

```js
// 设置平面样式
view = view3d(...) <<
    xPlaneRear: <<
        fillOpacity: 0.1,
        fillColor: 'red'
    >>,
    yPlaneRear: <<
        fillOpacity: 0.1,
        fillColor: 'green'
    >>,
    zPlaneRear: <<
        fillOpacity: 0.1,
        fillColor: 'blue'
    >>
>>;
```

## 示例

### 1. 创建基本 3D 视图（边框坐标轴）

```js
// 基本的 3D 视图，坐标轴在边框
view = view3d(
    [[-4, -4], [8, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'border'
>>;
```

### 2. 中心坐标轴

```js
// 坐标轴从原点显示
view = view3d(
    [[-6, -3], [8, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'center',
    withLabel: true
>>;

// 原点会自动标记为 O
```

### 3. 带透明平面的 3D 视图

```js
// 创建带半透明参考平面的 3D 视图
view = view3d(
    [[-6, -3], [8, 8]],
    [[-3, 3], [-3, 3], [-3, 3]]
) <<
    depthOrder: << enabled: true >>,
    projection: 'central',
    xPlaneRear: << fillOpacity: 0.2, fillColor: 'red' >>,
    yPlaneRear: << fillOpacity: 0.2, fillColor: 'green' >>,
    zPlaneRear: << fillOpacity: 0.2, fillColor: 'blue' >>
>>;
```

### 4. 平行投影与中心投影

```js
// 平行投影（等轴测视图）
viewParallel = view3d(
    [[-6, -3], [8, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    projection: 'parallel',
    axesPosition: 'border'
>>;

// 中心投影（透视视图）
viewPerspective = view3d(
    [[-6, -3], [8, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    projection: 'central',
    axesPosition: 'center'
>>;
```

### 5. 完整的 3D 场景

```js
// 创建 3D 视图
bound = [-5, 5];
view = view3d(
    [[-6, -4], [10, 8]],
    [[bound[0], bound[1]], [bound[0], bound[1]], [bound[0], bound[1]]]
) <<
    axesPosition: 'center',
    withLabel: true,
    xPlaneRear: << fillOpacity: 0.1 >>,
    yPlaneRear: << fillOpacity: 0.1 >>,
    zPlaneRear: << fillOpacity: 0.1 >>
>>;

// 添加 3D 点
A = view.create('point3d', [1, 2, 3]) << name: 'A', size: 5 >>;
B = view.create('point3d', [-2, 1, 4]) << name: 'B', size: 5 >>;

// 添加 3D 直线
l = view.create('line3d', [A, B]);
```

### 6. 自定义坐标轴样式

```js
// 自定义坐标轴颜色和线宽
view = view3d(
    [[-4, -4], [8, 8]],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    axesPosition: 'border',
    xAxis: << strokeColor: 'red', strokeWidth: 2 >>,
    yAxis: << strokeColor: 'green', strokeWidth: 2 >>,
    zAxis: << strokeColor: 'blue', strokeWidth: 2 >>
>>;
```

## 注意事项

1. **坐标轴位置**：`axesPosition: 'border'` 将坐标轴放在视图边框，`'center'` 从原点显示
2. **投影类型**：`projection: 'parallel'` 为平行投影，`'central'` 为透视投影
3. **深度排序**：设置 `depthOrder: << enabled: true >>` 可正确处理 3D 元素的遮挡关系
4. **平面透明度**：使用 `fillOpacity` 设置参考平面的透明度，便于观察内部元素
5. **标签显示**：`withLabel: true` 显示 x、y、z 轴标签

## 相关元素

- [Axis3D](./Axis3D.md) - 3D 单轴
- [Point3D](./Point3D.md) - 3D 点
- [Line3D](./Line3D.md) - 3D 直线
- [Curve3D](./Curve3D.md) - 3D 曲线
- [Circle3D](./Circle3D.md) - 3D 圆
