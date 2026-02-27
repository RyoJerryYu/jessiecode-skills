# Face3D 3D 面

## 描述

此元素创建一个 3D 面。

*定义于：* [face3d.js](./src/src_3d_face3d.js.md)
*继承自* [Curve](./Curve.md)

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
&nbsp;&nbsp;&nbsp;↳ **[JXG.Curve](./JXG.Curve.md)**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ **[Curve](./Curve.md)**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ **Face3D**

## JessieCode 语法

```js
// Face3D 元素没有直接构造函数
// 需要通过 Polyhedron3D 自动创建
// Face3D 是 Polyhedron3D 的面元素
```

## 构造函数

| 构造函数属性 | 构造函数名称和描述 |
| --- | --- |
| | **[Face3D](./Face3D.md#constructor)** | 一个 3D 面，待补充 |

### 抛出异常

- 抛出：{Exception} 如果无法使用给定的父对象构造元素，则抛出异常

## 属性

### 主要属性

| 属性 | 类型 | 描述 |
| --- | --- |
| | **[shader](./Face3D.md#shader)** | 面的着色 |

### shader {Object}

面的着色。为此，使用 HSL 颜色方案。

有两种类型：'angle' 或 'zIndex'。

默认情况下（即 type:'angle'），相机轴与面法线之间的角度决定 HSL 颜色的亮度值。否则，面的 zIndex 决定 HSL 颜色的亮度值。

*定义于：* [options3d.js](./src/src_options3d.js.md)

#### 参见

- [View3D#depthOrder](./View3D.md#depthOrder)

#### 默认值

```
{
  enabled: false,
  type: 'angle',   // 'angle'，否则 'zIndex'
  hue: 60,         // 黄色
  saturation: 90,
  minLightness: 30,
  maxLightness: 90
}
```

## 字段

| 字段 | 类型 | 描述 |
| --- | --- |
| | **[d](./Face3D.md#d)** | 包含面的平面的 Hesse 右侧值 |
| | **[faceNumber](./Face3D.md#faceNumber)** | 面在多面体面列表中的索引 |
| | **[normal](./Face3D.md#normal)** | 面的法向量 |
| | **[polyhedron](./Face3D.md#polyhedron)** | 与父多面体定义数据的链接 |
| | **[vec1](./Face3D.md#vec1)** | 面的第一个基向量 |
| | **[vec2](./Face3D.md#vec2)** | 面的第二个基向量 |

### d {Number}

包含面的平面的 Hesse 右侧值。

### faceNumber {Number}

面在多面体面列表中的索引

### normal {Array}

面的法向量。长度为 4 的数组。

### polyhedron {Object}

与父多面体定义数据的链接。

#### 参见

- [Polyhedron3D#def](./Polyhedron3D.md#def)

### vec1 {Array}

面的第一个基向量。长度为 4 的向量。

### vec2 {Array}

面的第二个基向量。长度为 4 的向量。

## 方法

| 方法 | 描述 |
| --- | --- |
| <static> | Face3D.**[shader](./Face3D.md#.shader)**() 确定面的亮度（在 HSL 颜色方案中） |
| | **[updateCoords](./Face3D.md#updateCoords)**() 更新多面体所有顶点的坐标 |
| | **[updateDataArray2D](./Face3D.md#updateDataArray2D)**() 更新面的 2D 坐标并确定其 z 索引 |

### <static> {Number} Face3D.shader()

确定面的亮度（在 HSL 颜色方案中）。

设置伴随 2D 曲线的 fillColor。

#### 返回值

- {Number} 面的 zIndex

### {[Face3D](./Face3D.md)} updateCoords()

更新多面体所有顶点的坐标

#### 返回值

- {[Face3D](./Face3D.md)} 返回自身的引用

### {Object} updateDataArray2D()

更新面的 2D 坐标并确定其 z 索引。

#### 返回值

- {Object} {X:[], Y:[]}

## 示例

### 1. 创建 3D 视图中的面

```js
// Face3D 通常作为 Polyhedron3D 的一部分自动创建
// 以下是通过 Polyhedron3D 创建面的示例

// 创建 3D 视图
box = [-5, 5];
view = view3d(
    [-6, -3], [8, 8],
    [box, box, box]
) <<
    xPlaneRear: {visible: false},
    yPlaneRear: {visible: false}
>>;

// 创建 3D 点作为顶点
p1 = view.create('point3d', [1, 0, 0]);
p2 = view.create('point3d', [0, 1, 0]);
p3 = view.create('point3d', [0, 0, 1]);
p4 = view.create('point3d', [-1, 0, 0]);

// 创建四面体（会自动创建 Face3D 面）
tetra = view.create('polyhedron3d', [[p1, p2, p3, p4]]);
```

### 2. 设置面的着色属性

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]
);

// 创建立方体的顶点
v1 = view.create('point3d', [1, 1, 1]);
v2 = view.create('point3d', [-1, 1, 1]);
v3 = view.create('point3d', [-1, -1, 1]);
v4 = view.create('point3d', [1, -1, 1]);
v5 = view.create('point3d', [1, 1, -1]);
v6 = view.create('point3d', [-1, 1, -1]);
v7 = view.create('point3d', [-1, -1, -1]);
v8 = view.create('point3d', [1, -1, -1]);

// 创建立方体（带有着色设置）
cube = view.create('polyhedron3d', [[v1, v2, v3, v4, v5, v6, v7, v8]]) <<
    faces: {
        shader: {
            enabled: true,
            type: 'angle',
            hue: 60,
            saturation: 90,
            minLightness: 30,
            maxLightness: 90
        }
    }
>>;
```

### 3. 使用 zIndex 着色

```js
// 创建 3D 视图
view = view3d(
    [-10, -5], [12, 12],
    [[-5, 5], [-5, 5], [-5, 5]]
);

// 创建多面体，使用 zIndex 着色
poly = view.create('polyhedron3d', [vertices]) <<
    faces: {
        shader: {
            enabled: true,
            type: 'zIndex',  // 根据深度着色
            hue: 200,        // 蓝色调
            saturation: 80,
            minLightness: 20,
            maxLightness: 80
        }
    }
>>;
```

### 4. 访问面的属性

```js
// 创建多面体后，可以访问其面
view = view3d([-6, -3], [8, 8], [[-5, 5], [-5, 5], [-5, 5]]);

// 创建四面体
tetra = view.create('polyhedron3d', [[p1, p2, p3, p4]]);

// 访问第一个面
face0 = tetra.faces[0];

// 获取面的法向量
normal = face0.normal;

// 获取面在多面体中的索引
index = face0.faceNumber;
```

## 注意事项

1. **Face3D 通常不直接创建**：Face3D 元素通常作为 Polyhedron3D（3D 多面体）的一部分自动创建
2. **着色效果**：shader 属性可以增强 3D 视觉效果，使面根据角度或深度呈现不同的明暗
3. **HSL 颜色方案**：着色使用 HSL（色调、饱和度、亮度）颜色方案
4. **两种着色类型**：
   - 'angle'：根据相机轴与面法线的角度决定亮度
   - 'zIndex'：根据面的深度（zIndex）决定亮度
5. **性能考虑**：启用着色可能会影响渲染性能

## 相关元素

- [Curve](./Curve.md) - 曲线（父类）
- [Polyhedron3D](./Polyhedron3D.md) - 3D 多面体
- [View3D](./View3D.md) - 3D 视图
