# IntersectionCircle3D 3D 圆交点

## 描述

3D 中两个元素（plane3d 或 sphere3d）相交形成的圆。

*定义于：* [circle3d.js](./src/src_3d_circle3d.js.md)
*继承自* [JXG.Circle3D](./JXG.Circle3D.md)

## 继承关系

**[JXG.Curve3D](./JXG.Curve3D.md), JXG.GeometryElement**
&nbsp;&nbsp;&nbsp;↳ **[JXG.Circle3D](./JXG.Circle3D.md)**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ **IntersectionCircle3D**

## JessieCode 语法

```js
// IntersectionCircle3D 元素没有直接构造函数
// 需要在 3D 视图中创建

// 基本语法（在 3D 视图中）
// view.create('intersectioncircle3d', [el1, el2])

// el1, el2 可以是 Sphere3D 或 Plane3D
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| el1 | Sphere3D/Plane3D | 第一个元素（球体或平面） |
| el2 | Sphere3D/Plane3D | 第二个元素（球体或平面） |

### 可相交的元素组合

| 元素 1 | 元素 2 | 说明 |
|--------|--------|------|
| Sphere3D | Sphere3D | 两个球体的交点圆 |
| Sphere3D | Plane3D | 球体与平面的交点圆 |
| Plane3D | Sphere3D | 平面与球体的交点圆 |

### 抛出异常

- 抛出：{Exception} 如果无法使用给定的父对象构造元素，则抛出异常

## 属性

IntersectionCircle3D 继承自 Circle3D，因此拥有 Circle3D 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `visible` | Boolean | true | 是否可见 |
| `dash` | Number | 0 | 虚线样式 |

## 示例

### 1. 两个球体的交点圆

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[0, 3], [0, 3], [0, 3]]
) <<
    xPlaneRear: {fillOpacity: 0.2, gradient: null},
    yPlaneRear: {fillOpacity: 0.2, gradient: null},
    zPlaneRear: {fillOpacity: 0.2, gradient: null}
>>;

// 创建两个 3D 点作为球心
a1 = view.create('point3d', [-1, 0, 0]);
a2 = view.create('point3d', [1, 0, 0]);

// 创建两个球体
s1 = view.create('sphere3d', [a1, 2]) <<
    fillColor: '#00ff80'
>>;

s2 = view.create('sphere3d', [a2, 2]) <<
    fillColor: '#ff0000'
>>;

// 创建交点圆
i = view.create('intersectioncircle3d', [s1, s2]);
```

### 2. 球体与平面的交点圆

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]
) <<
    xPlaneRear: {visible: true, fillOpacity: 0.1},
    yPlaneRear: {visible: true, fillOpacity: 0.1},
    zPlaneRear: {visible: true, fillOpacity: 0.1}
>>;

// 创建球心
center = view.create('point3d', [0, 0, 0]);

// 创建球体（半径 3）
sphere = view.create('sphere3d', [center, 3]) <<
    fillColor: 'blue',
    fillOpacity: 0.5
>>;

// 创建平面（z = 1，与球体相交）
// 平面由一个点和两个方向向量定义
p = view.create('point3d', [0, 0, 1]);
v1 = view.create('point3d', [1, 0, 1]);
v2 = view.create('point3d', [0, 1, 1]);
plane = view.create('plane3d', [p, v1, v2]) <<
    fillColor: 'yellow',
    fillOpacity: 0.3
>>;

// 创建交点圆
circle = view.create('intersectioncircle3d', [sphere, plane]) <<
    strokeColor: 'red',
    strokeWidth: 3
>>;
```

### 3. 不同半径的球体交点

```js
// 创建 3D 视图
view = view3d(
    [-8, -4], [10, 10],
    [[-3, 5], [-3, 3], [-3, 3]]
);

// 创建两个不同半径的球体
c1 = view.create('point3d', [-1, 0, 0]);
c2 = view.create('point3d', [1, 0, 0]);

s1 = view.create('sphere3d', [c1, 2.5]) <<
    fillColor: 'cyan',
    fillOpacity: 0.4
>>;

s2 = view.create('sphere3d', [c2, 1.5]) <<
    fillColor: 'magenta',
    fillOpacity: 0.4
>>;

// 创建交点圆
i = view.create('intersectioncircle3d', [s1, s2]) <<
    strokeColor: 'white',
    strokeWidth: 4
>>;
```

### 4. 多个相交球体

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-2, 4], [-2, 4], [-2, 4]]
);

// 创建三个球体
c1 = view.create('point3d', [0, 0, 0]);
c2 = view.create('point3d', [2, 0, 0]);
c3 = view.create('point3d', [1, 2, 0]);

s1 = view.create('sphere3d', [c1, 2]) << fillColor: 'red', fillOpacity: 0.3 >>;
s2 = view.create('sphere3d', [c2, 2]) << fillColor: 'green', fillOpacity: 0.3 >>;
s3 = view.create('sphere3d', [c3, 2]) << fillColor: 'blue', fillOpacity: 0.3 >>;

// 创建交点圆
i12 = view.create('intersectioncircle3d', [s1, s2]) << strokeColor: 'yellow' >>;
i23 = view.create('intersectioncircle3d', [s2, s3]) << strokeColor: 'cyan' >>;
i13 = view.create('intersectioncircle3d', [s1, s3]) << strokeColor: 'magenta' >>;
```

### 5. 平面切割球体

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-4, 4], [-4, 4], [-4, 4]]
);

// 创建球体
sphere = view.create('sphere3d', [
    view.create('point3d', [0, 0, 0]),
    3
]) << fillColor: 'orange', fillOpacity: 0.5 >>;

// 创建不同角度的切割平面
// 水平平面
p1 = view.create('point3d', [0, 0, 1]);
v1a = view.create('point3d', [1, 0, 1]);
v1b = view.create('point3d', [0, 1, 1]);
plane1 = view.create('plane3d', [p1, v1a, v1b]) << fillColor: 'white', fillOpacity: 0.2 >>;
circle1 = view.create('intersectioncircle3d', [sphere, plane1]) << strokeColor: 'red', strokeWidth: 3 >>;

// 垂直平面
p2 = view.create('point3d', [1, 0, 0]);
v2a = view.create('point3d', [1, 1, 0]);
v2b = view.create('point3d', [1, 0, 1]);
plane2 = view.create('plane3d', [p2, v2a, v2b]) << fillColor: 'gray', fillOpacity: 0.2 >>;
circle2 = view.create('intersectioncircle3d', [sphere, plane2]) << strokeColor: 'blue', strokeWidth: 3 >>;
```

### 6. 动态球体交点

```js
// 创建滑块控制球心位置
sliderX = slider([-2, 4], [4, 4], [-1.5, 0, 1.5]) << name: 'x' >>;

// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-3, 5], [-3, 3], [-3, 3]]
);

// 固定球心
c1 = view.create('point3d', [0, 0, 0]);

// 动态球心（x 坐标由滑块控制）
c2 = view.create('point3d', [
    () => V(sliderX),
    0,
    0
]);

// 创建球体
s1 = view.create('sphere3d', [c1, 2]) << fillColor: 'red', fillOpacity: 0.4 >>;
s2 = view.create('sphere3d', [c2, 2]) << fillColor: 'blue', fillOpacity: 0.4 >>;

// 交点圆会随滑块移动而动态变化
i = view.create('intersectioncircle3d', [s1, s2]) <<
    strokeColor: 'white',
    strokeWidth: 4
>>;
```

### 7. 相切情况

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-1, 5], [-3, 3], [-3, 3]]
);

// 创建两个相切的球体（距离等于半径之和）
c1 = view.create('point3d', [0, 0, 0]);
c2 = view.create('point3d', [3, 0, 0]);  // 距离为 3

s1 = view.create('sphere3d', [c1, 1.5]) << fillColor: 'red', fillOpacity: 0.4 >>;
s2 = view.create('sphere3d', [c2, 1.5]) << fillColor: 'blue', fillOpacity: 0.4 >>;

// 相切时交点圆退化为一个点
i = view.create('intersectioncircle3d', [s1, s2]) <<
    strokeColor: 'yellow',
    strokeWidth: 4
>>;
```

### 8. 球体与倾斜平面

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-4, 4], [-4, 4], [-4, 4]]
);

// 创建球体
sphere = view.create('sphere3d', [
    view.create('point3d', [0, 0, 0]),
    3
]) << fillColor: 'cyan', fillOpacity: 0.5 >>;

// 创建倾斜平面
p = view.create('point3d', [0, 0, 0]);
v1 = view.create('point3d', [1, 0, 1]);  // 倾斜方向 1
v2 = view.create('point3d', [0, 1, 0]);  // 方向 2
plane = view.create('plane3d', [p, v1, v2]) <<
    fillColor: 'yellow',
    fillOpacity: 0.3
>>;

// 创建交点圆
circle = view.create('intersectioncircle3d', [sphere, plane]) <<
    strokeColor: 'red',
    strokeWidth: 3
>>;
```

## 注意事项

1. **相交条件**：
   - 两个球体：球心距离必须小于半径之和且大于半径之差
   - 球体与平面：平面必须与球体相交（球心到平面的距离小于半径）

2. **特殊情况**：
   - 相切时，交点圆退化为一个点
   - 不相交时，可能无法创建或创建不可见的圆

3. **3D 视图**：IntersectionCircle3D 必须在 3D 视图（view3d）中创建

4. **视觉属性**：可以设置 strokeColor、strokeWidth 等属性来增强可见性

5. **性能**：复杂的 3D 计算可能影响性能

## 相关元素

- [Circle3D](./Circle3D.md) - 3D 圆（父类）
- [Sphere3D](./Sphere3D.md) - 3D 球体
- [Plane3D](./Plane3D.md) - 3D 平面
- [View3D](./View3D.md) - 3D 视图
