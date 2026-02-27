# IntersectionLine3D 3D 直线交点

<!-- USAGE_FREQUENCY: advanced -->

## 描述

3D 中两个（无限）平面元素相交形成的直线。

*定义于：* [linspace3d.js](./src/src_3d_linspace3d.js.md)
*继承自* [JXG.Line3D](./JXG.Line3D.md)

## 继承关系

**[JXG.GeometryElement3D](./JXG.GeometryElement3D.md), JXG.GeometryElement**
&nbsp;&nbsp;&nbsp;↳ **[JXG.Line3D](./JXG.Line3D.md)**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ **IntersectionLine3D**

## JessieCode 语法

```js
// IntersectionLine3D 元素没有直接构造函数
// 需要在 3D 视图中创建

// 基本语法（在 3D 视图中）
// view.create('intersectionline3d', [el1, el2])

// el1, el2 必须是 Plane3D
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| el1 | Plane3D | 第一个平面 |
| el2 | Plane3D | 第二个平面 |

### 可相交的元素组合

| 元素 1 | 元素 2 | 说明 |
|--------|--------|------|
| Plane3D | Plane3D | 两个平面的交线 |

### 抛出异常

- 抛出：{Exception} 如果无法使用给定的父对象构造元素，则抛出异常

## 属性

IntersectionLine3D 继承自 Line3D，因此拥有 Line3D 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `visible` | Boolean | true | 是否可见 |
| `dash` | Number | 0 | 虚线样式 |
| `firstArrow` | Boolean/Object | false | 起点箭头 |
| `lastArrow` | Boolean/Object | false | 终点箭头 |

## 示例

### 1. 两个平面的交线

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-1, 3], [-1, 3], [-1, 3]]
) <<
    xPlaneRear: {visible: false},
    yPlaneRear: {visible: false},
    zPlaneRear: {fillOpacity: 0.2, gradient: null}
>>;

// 创建一个 3D 点
a = view.create('point3d', [2, 2, 0]);

// 创建第一个平面（xy 平面）
p1 = view.create('plane3d', [a, [1, 0, 0], [0, 1, 0]]) <<
    fillColor: '#00ff80'
>>;

// 创建第二个平面（倾斜平面）
p2 = view.create('plane3d', [a, [-2, 1, 1], [1, -2, 1]]) <<
    fillColor: '#ff0000'
>>;

// 创建交线
i = view.create('intersectionline3d', [p1, p2]);
```

### 2. 垂直平面的交线

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

// 创建原点
o = view.create('point3d', [0, 0, 0]);

// xy 平面（z = 0）
p1 = view.create('plane3d', [o, [1, 0, 0], [0, 1, 0]]) <<
    fillColor: 'red',
    fillOpacity: 0.3
>>;

// xz 平面（y = 0）
p2 = view.create('plane3d', [o, [1, 0, 0], [0, 0, 1]]) <<
    fillColor: 'green',
    fillOpacity: 0.3
>>;

// 交线是 x 轴
i = view.create('intersectionline3d', [p1, p2]) <<
    strokeColor: 'blue',
    strokeWidth: 4
>>;
```

### 3. 三个平面两两相交

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-4, 4], [-4, 4], [-4, 4]]
);

// 创建三个平面
o = view.create('point3d', [0, 0, 0]);

// xy 平面
p1 = view.create('plane3d', [o, [1, 0, 0], [0, 1, 0]]) <<
    fillColor: 'red', fillOpacity: 0.2 >>;

// yz 平面
p2 = view.create('plane3d', [o, [0, 1, 0], [0, 0, 1]]) <<
    fillColor: 'green', fillOpacity: 0.2 >>;

// xz 平面
p3 = view.create('plane3d', [o, [1, 0, 0], [0, 0, 1]]) <<
    fillColor: 'blue', fillOpacity: 0.2 >>;

// 三条交线（坐标轴）
xAxis = view.create('intersectionline3d', [p2, p3]) << strokeColor: 'red', strokeWidth: 3 >>;
yAxis = view.create('intersectionline3d', [p1, p3]) << strokeColor: 'green', strokeWidth: 3 >>;
zAxis = view.create('intersectionline3d', [p1, p2]) << strokeColor: 'blue', strokeWidth: 3 >>;
```

### 4. 平行平面（无交线）

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-4, 4], [-4, 4], [-4, 4]]
);

// 创建两个平行平面（没有交线）
o = view.create('point3d', [0, 0, 0]);
p1 = view.create('point3d', [0, 0, 2]);  // z = 2 的点

// xy 平面（z = 0）
plane1 = view.create('plane3d', [o, [1, 0, 0], [0, 1, 0]]) <<
    fillColor: 'red', fillOpacity: 0.3 >>;

// 平行平面（z = 2）
plane2 = view.create('plane3d', [p1, [1, 0, 0], [0, 1, 0]]) <<
    fillColor: 'blue', fillOpacity: 0.3 >>;

// 注意：平行平面没有交线，创建会失败或返回空
// i = view.create('intersectionline3d', [plane1, plane2]);  // 会抛出异常
```

### 5. 动态平面交线

```js
// 创建滑块控制平面角度
angleSlider = slider([0, 4], [4, 4], [0, 0, PI]) << name: '角度' >>;

// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-4, 4], [-4, 4], [-4, 4]]
);

// 固定平面（xy 平面）
o = view.create('point3d', [0, 0, 0]);
p1 = view.create('plane3d', [o, [1, 0, 0], [0, 1, 0]]) <<
    fillColor: 'red', fillOpacity: 0.2 >>;

// 动态平面（绕 x 轴旋转）
p2 = view.create('plane3d', [
    o,
    [1, 0, 0],  // x 轴方向固定
    () => [0, cos(V(angleSlider)), sin(V(angleSlider))]  // 旋转方向
]) <<
    fillColor: 'blue', fillOpacity: 0.2 >>;

// 交线会随滑块动态变化
i = view.create('intersectionline3d', [p1, p2]) <<
    strokeColor: 'green',
    strokeWidth: 4
>>;
```

### 6. 一般位置的平面

```js
// 创建 3D 视图
view = view3d(
    [-8, -4], [10, 10],
    [[-5, 5], [-5, 5], [-5, 5]]
);

// 创建一般位置的平面
// 平面 1：通过点 (1, 0, 0)，方向向量 (0, 1, 1) 和 (1, 0, 1)
p1 = view.create('point3d', [1, 0, 0]);
v1a = view.create('point3d', [1, 1, 1]);
v1b = view.create('point3d', [2, 0, 1]);
plane1 = view.create('plane3d', [p1, v1a, v1b]) <<
    fillColor: 'cyan', fillOpacity: 0.3 >>;

// 平面 2：通过点 (0, 1, 0)，方向向量 (1, 0, 1) 和 (0, 1, 1)
p2 = view.create('point3d', [0, 1, 0]);
v2a = view.create('point3d', [1, 1, 1]);
v2b = view.create('point3d', [0, 2, 1]);
plane2 = view.create('plane3d', [p2, v2a, v2b]) <<
    fillColor: 'magenta', fillOpacity: 0.3 >>;

// 创建交线
i = view.create('intersectionline3d', [plane1, plane2]) <<
    strokeColor: 'yellow',
    strokeWidth: 4
>>;
```

### 7. 平面与坐标平面

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-4, 4], [-4, 4], [-4, 4]]
);

// 创建坐标平面
o = view.create('point3d', [0, 0, 0]);

// xy 平面
xyPlane = view.create('plane3d', [o, [1, 0, 0], [0, 1, 0]]) <<
    fillColor: 'red', fillOpacity: 0.1 >>;

// 创建倾斜平面
tiltedPlane = view.create('plane3d', [
    view.create('point3d', [0, 0, 2]),
    view.create('point3d', [1, 0, 2]),
    view.create('point3d', [0, 1, 0])
]) <<
    fillColor: 'blue', fillOpacity: 0.3 >>;

// 与 xy 平面的交线
i = view.create('intersectionline3d', [xyPlane, tiltedPlane]) <<
    strokeColor: 'green',
    strokeWidth: 3,
    lastArrow: true
>>;
```

### 8. 带箭头的交线

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-4, 4], [-4, 4], [-4, 4]]
);

// 创建两个平面
o = view.create('point3d', [0, 0, 0]);
p1 = view.create('plane3d', [o, [1, 0, 0], [0, 1, 0]]) <<
    fillColor: 'red', fillOpacity: 0.2 >>;
p2 = view.create('plane3d', [o, [0, 1, 0], [0, 0, 1]]) <<
    fillColor: 'blue', fillOpacity: 0.2 >>;

// 创建带双向箭头的交线
i = view.create('intersectionline3d', [p1, p2]) <<
    strokeColor: 'green',
    strokeWidth: 3,
    firstArrow: true,
    lastArrow: true
>>;
```

### 9. 平面方程表示

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-4, 4], [-4, 4], [-4, 4]]
);

// 平面 1: x + y + z = 3
// 通过点 (3,0,0), 方向向量 (-1,1,0) 和 (-1,0,1)
p1a = view.create('point3d', [3, 0, 0]);
p1b = view.create('point3d', [2, 1, 0]);
p1c = view.create('point3d', [2, 0, 1]);
plane1 = view.create('plane3d', [p1a, p1b, p1c]) <<
    fillColor: 'red', fillOpacity: 0.2 >>;

// 平面 2: x - y + z = 1
// 通过点 (1,0,0), 方向向量 (1,1,0) 和 (1,0,-1)
p2a = view.create('point3d', [1, 0, 0]);
p2b = view.create('point3d', [2, 1, 0]);
p2c = view.create('point3d', [2, 0, -1]);
plane2 = view.create('plane3d', [p2a, p2b, p2c]) <<
    fillColor: 'blue', fillOpacity: 0.2 >>;

// 创建交线
i = view.create('intersectionline3d', [plane1, plane2]) <<
    strokeColor: 'yellow',
    strokeWidth: 4
>>;
```

### 10. 多个相交平面

```js
// 创建 3D 视图
view = view3d(
    [-6, -3], [8, 8],
    [[-4, 4], [-4, 4], [-4, 4]]
);

// 创建中心点
o = view.create('point3d', [0, 0, 0]);

// 创建四个通过原点的平面
// 平面 1：xy 平面
p1 = view.create('plane3d', [o, [1, 0, 0], [0, 1, 0]]) <<
    fillColor: 'red', fillOpacity: 0.15 >>;

// 平面 2：与 xy 平面成 45 度
p2 = view.create('plane3d', [o, [1, 0, 0], [0, 1, 1]]) <<
    fillColor: 'green', fillOpacity: 0.15 >>;

// 平面 3：与 xy 平面成 90 度（yz 平面）
p3 = view.create('plane3d', [o, [0, 1, 0], [0, 0, 1]]) <<
    fillColor: 'blue', fillOpacity: 0.15 >>;

// 平面 4：与 xy 平面成 135 度
p4 = view.create('plane3d', [o, [0, 1, 0], [1, 0, -1]]) <<
    fillColor: 'yellow', fillOpacity: 0.15 >>;

// 创建所有交线
l12 = view.create('intersectionline3d', [p1, p2]) << strokeColor: 'cyan' >>;
l23 = view.create('intersectionline3d', [p2, p3]) << strokeColor: 'magenta' >>;
l34 = view.create('intersectionline3d', [p3, p4]) << strokeColor: 'orange' >>;
l14 = view.create('intersectionline3d', [p1, p4]) << strokeColor: 'purple' >>;
```

## 注意事项

1. **相交条件**：两个平面必须不平行才能相交。平行平面没有交线

2. **平面定义**：平面由一个点和两个方向向量定义

3. **3D 视图**：IntersectionLine3D 必须在 3D 视图（view3d）中创建

4. **视觉属性**：可以设置 strokeColor、strokeWidth、dash 等属性来增强可见性

5. **箭头**：可以使用 firstArrow 和 lastArrow 属性在交线两端添加箭头

6. **性能**：复杂的 3D 计算可能影响性能

7. **异常处理**：当平面平行时，创建交线会抛出异常

## 相关元素

- [Line3D](./Line3D.md) - 3D 直线（父类）
- [Plane3D](./Plane3D.md) - 3D 平面
- [View3D](./View3D.md) - 3D 视图
- [IntersectionCircle3D](./IntersectionCircle3D.md) - 3D 圆交点
