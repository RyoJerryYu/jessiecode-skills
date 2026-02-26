# ParametricSurface3D 3D 参数曲面

## 描述

3D 参数曲面可视化一个映射 (u, v) → [X(u, v), Y(u, v), Z(u, v)]，即通过参数方程定义的三维曲面。

## JessieCode 语法

```js
// 通过三个函数创建参数曲面
surface = parametricsurface3d(FX, FY, FZ, rangeU, rangeV);

// 通过一个返回数组的函数创建参数曲面
surface = parametricsurface3d(F, rangeU, rangeV);

// 带属性创建
surface = parametricsurface3d(
    (u, v) => sin(u) * cos(v),
    (u, v) => sin(u) * sin(v),
    (u, v) => cos(u),
    [0, 2*PI],
    [0, PI]
) <<
    strokeColor: 'red',
    stepsU: 30,
    stepsV: 30
>>;

// 在 3D 视图中创建
view = view3d([-6, -3], [8, 8], [[-5, 5], [-5, 5], [-5, 5]]);
surface = view.create('parametricsurface3d', [...]);
```

## 参数

### 方式一：三个坐标函数

| 参数 | 类型 | 描述 |
|------|------|------|
| FX | Function | 函数 FX(u, v)，返回 x 坐标 |
| FY | Function | 函数 FY(u, v)，返回 y 坐标 |
| FZ | Function | 函数 FZ(u, v)，返回 z 坐标 |
| rangeU | Array/Function | 参数 u 的范围 [min, max]，也可以是返回数组的函数 |
| rangeV | Array/Function | 参数 v 的范围 [min, max]，也可以是返回数组的函数 |

### 方式二：向量值函数

| 参数 | 类型 | 描述 |
|------|------|------|
| F | Function | 函数 F(u, v)，返回数组 [x, y, z] |
| rangeU | Array/Function | 参数 u 的范围 [min, max] |
| rangeV | Array/Function | 参数 v 的范围 [min, max] |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 1 | 描边宽度 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `fillOpacity` | Number | 0.5 | 填充透明度 |
| `stepsU` | Number | 20 | 参数 u 方向的网格分割数 |
| `stepsV` | Number | 20 | 参数 v 方向的网格分割数 |
| `visible` | Boolean | true | 是否可见 |

## 方法

ParametricSurface3D 继承自 Curve，具有以下常用方法：

| 方法 | 参数 | 描述 |
|------|------|------|
| `X()` | 无 | 获取当前点的 x 坐标 |
| `Y()` | 无 | 获取当前点的 y 坐标 |
| `Z()` | 无 | 获取当前点的 z 坐标 |
| `Value(t)` | t: Number | 获取参数 t 处的值 |

## 示例

### 1. 创建球面

```js
view = view3d([-6, -3], [8, 8], [[-5, 5], [-5, 5], [-5, 5]]);

// 半径为 2 的球面
c = view.create('parametricsurface3d', [
    (u, v) => 2 * Math.sin(u) * Math.cos(v),
    (u, v) => 2 * Math.sin(u) * Math.sin(v),
    (u, v) => 2 * Math.cos(u),
    [0, 2 * Math.PI],
    [0, Math.PI]
], <<
    strokeColor: '#ff0000',
    stepsU: 30,
    stepsV: 30
>>);
```

### 2. 创建环面（甜甜圈形状）

```js
view = view3d([-6, -3], [8, 8], [[-5, 5], [-5, 5], [-5, 5]]);

// 环面参数方程
// R = 2（大半径），r = 0.8（小半径）
R = 2;
r = 0.8;

torus = view.create('parametricsurface3d', [
    (u, v) => (R + r * cos(u)) * cos(v),
    (u, v) => (R + r * cos(u)) * sin(v),
    (u, v) => r * sin(u),
    [0, 2*PI],
    [0, 2*PI]
], <<
    fillColor: 'yellow',
    fillOpacity: 0.7,
    strokeColor: 'orange',
    stepsU: 40,
    stepsV: 40
>>);
```

### 3. 创建螺旋面

```js
view = view3d([-6, -3], [8, 8], [[-5, 5], [-5, 5], [-5, 5]]);

// 螺旋面
helix = view.create('parametricsurface3d', [
    (u, v) => v * cos(u),
    (u, v) => v * sin(u),
    (u, v) => u,
    [0, 4*PI],
    [0, 2]
], <<
    fillColor: 'blue',
    fillOpacity: 0.6,
    stepsU: 50,
    stepsV: 20
>>);
```

### 4. 创建马鞍面（双曲抛物面）

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]]);

// 马鞍面 z = x^2 - y^2
saddle = view.create('parametricsurface3d', [
    (u, v) => u,
    (u, v) => v,
    (u, v) => u*u - v*v,
    [-2, 2],
    [-2, 2]
], <<
    fillColor: 'green',
    fillOpacity: 0.5,
    stepsU: 30,
    stepsV: 30
>>);
```

### 5. 使用向量值函数创建曲面

```js
view = view3d([-6, -3], [8, 8], [[-5, 5], [-5, 5], [-5, 5]]);

// 使用单个函数返回 [x, y, z] 数组
sphere = view.create('parametricsurface3d', [
    (u, v) => [
        2 * sin(u) * cos(v),
        2 * sin(u) * sin(v),
        2 * cos(u)
    ],
    [0, 2*PI],
    [0, PI]
], <<
    fillColor: 'cyan',
    fillOpacity: 0.6
>>);
```

### 6. 动态参数曲面

```js
view = view3d([-6, -3], [8, 8], [[-5, 5], [-5, 5], [-5, 5]]);

// 创建滑块控制振幅
a = slider(0, 2, 0.1, << name: '振幅' >>);

// 波浪曲面
wave = view.create('parametricsurface3d', [
    (u, v) => u,
    (u, v) => v,
    (u, v) => V(a) * sin(u) * cos(v),
    [-3, 3],
    [-3, 3]
], <<
    fillColor: 'purple',
    fillOpacity: 0.6,
    stepsU: 40,
    stepsV: 40
>>);
```

### 7. 创建圆锥面

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]]);

// 圆锥面
cone = view.create('parametricsurface3d', [
    (u, v) => v * cos(u),
    (u, v) => v * sin(u),
    (u, v) => v,
    [0, 2*PI],
    [0, 3]
], <<
    fillColor: 'orange',
    fillOpacity: 0.7,
    stepsU: 40,
    stepsV: 20
>>);
```

### 8. 创建柱面

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]]);

// 圆柱面（半径为 2）
cylinder = view.create('parametricsurface3d', [
    (u, v) => 2 * cos(u),
    (u, v) => 2 * sin(u),
    (u, v) => v,
    [0, 2*PI],
    [-3, 3]
], <<
    fillColor: 'pink',
    fillOpacity: 0.5,
    stepsU: 40,
    stepsV: 20
>>);
```

## 注意事项

1. **网格密度**：`stepsU` 和 `stepsV` 控制曲面的网格密度，值越大曲面越平滑，但计算量也越大
2. **参数范围**：确保参数范围正确，以避免曲面显示不完整或重复
3. **函数性能**：坐标函数会被频繁调用，应避免在函数中执行复杂计算
4. **3D 视图**：参数曲面必须在 3D 视图（view3d）中创建和显示
5. **透明度**：适当设置 `fillOpacity` 可以更好地观察曲面内部结构

## 相关元素

- [Curve](./Curve.md) - 曲线
- [Point3D](./Point3D.md) - 3D 点
- [View3D](./View3D.md) - 3D 视图
- [Sphere3D](./Sphere3D.md) - 3D 球面
