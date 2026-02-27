# Plane3D 3D 平面

<!-- USAGE_FREQUENCY: advanced -->

## 描述

3D 平面由一个点和两个线性无关的向量定义，或者由三个点定义。

## JessieCode 语法

```js
// 通过一个点和两个方向向量创建平面
plane = plane3d(point, direction1, direction2);

// 通过一个点、两个方向向量和范围创建有限平面
plane = plane3d(point, direction1, direction2, range1, range2);

// 通过三个点创建平面
plane = plane3d(point1, point2, point3);

// 带属性创建
plane = plane3d(A, [1, 0, 0], [0, 1, 0]) <<
    fillColor: 'blue',
    fillOpacity: 0.3
>>;

// 在 3D 视图中创建
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]]);
plane = view.create('plane3d', [A, [1, 0, 0], [0, 1, 0]]);
```

## 参数

### 方式一：点 + 两个方向向量

| 参数 | 类型 | 描述 |
|------|------|------|
| point | Point3D/Array/Function | 平面上的一个点（Point3D 元素或长度为 3 的数组） |
| direction1 | Line3D/Array/Function | 第一个方向向量（line3d 元素、长度为 3 的数组或返回数组的函数） |
| direction2 | Line3D/Array/Function | 第二个方向向量（line3d 元素、长度为 3 的数组或返回数组的函数） |
| range1 | Array/Function | （可选）方向向量 1 的范围 [r1, r2]，使用 [-Infinity, Infinity] 表示无限延伸 |
| range2 | Array/Function | （可选）方向向量 2 的范围 [r1, r2]，使用 [-Infinity, Infinity] 表示无限延伸 |

### 方式二：三个点

| 参数 | 类型 | 描述 |
|------|------|------|
| point1 | Point3D/Array/Function | 第一个点 |
| point2 | Point3D/Array/Function | 第二个点 |
| point3 | Point3D/Array/Function | 第三个点 |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `fillOpacity` | Number | 0.1 | 填充透明度 |
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 1 | 描边宽度 |
| `visible` | Boolean | true | 是否可见 |

### 点属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `point` | Point3D | visible: false, name: "", fixed: true | 定义点的属性（点 + 方向向量方式） |
| `point1` | Point3D | visible: false, name: "" | 第一个点的属性（三点方式） |
| `point2` | Point3D | visible: false, name: "" | 第二个点的属性（三点方式） |
| `point3` | Point3D | visible: false, name: "" | 第三个点的属性（三点方式） |
| `threePoints` | Boolean | false | 若为 true，第二和第三参数解释为点坐标而非方向向量 |

### 网格属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `mesh3d` | Mesh3D | 见 Mesh3D | 有限平面的可选 3D 网格 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `F(u, v)` | u, v: Number | 获取平面上参数为 (u, v) 的点的坐标数组 [x, y, z] |
| `X(u, v)` | u, v: Number | 获取平面上参数为 (u, v) 的点的 x 坐标 |
| `Y(u, v)` | u, v: Number | 获取平面上参数为 (u, v) 的点的 y 坐标 |
| `Z(u, v)` | u, v: Number | 获取平面上参数为 (u, v) 的点的 z 坐标 |

## 示例

### 1. 创建无限平面（点和方向向量）

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]], <<
    depthOrder: << enabled: true >>,
    projection: 'central',
    xPlaneRear: << fillOpacity: 0.2 >>,
    yPlaneRear: << fillOpacity: 0.2 >>,
    zPlaneRear: << fillOpacity: 0.2 >>
>>);

// 创建一个点
A = view.create('point3d', [-2, 0, 1], << size: 2 >>);

// 通过点和两个方向创建无限平面
plane = view.create('plane3d', [
    A,
    [1, 0, 0],
    [0, 1, 0],
    [-Infinity, Infinity],
    [-Infinity, Infinity]
]);
```

### 2. 创建有限平面（点和方向向量）

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]], <<
    depthOrder: << enabled: true >>,
    projection: 'central'
>>);

A = view.create('point3d', [-2, 0, 1], << size: 2 >>);

// 有限平面，范围 [-2, 2] x [-2, 2]
plane1 = view.create('plane3d', [
    A,
    [1, 0, 0],
    [0, 1, 0],
    [-2, 2],
    [-2, 2]
]);

// 带网格和可见定义点的平面
plane2 = view.create('plane3d', [
    [0, 0, -1],
    [1, 0, 0],
    [0, 1, 0],
    [-2, 2],
    [-2, 2]
], <<
    mesh3d: << visible: true >>,
    point: << visible: true, name: "B", fixed: false >>
>>);
```

### 3. 使用 3D 直线作为方向向量

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]], <<
    depthOrder: << enabled: true >>,
    projection: 'central',
    xPlaneRear: << visible: false, fillOpacity: 0.2 >>,
    yPlaneRear: << visible: false, fillOpacity: 0.2 >>,
    zPlaneRear: << fillOpacity: 0.2 >>
>>);

A = view.create('point3d', [-2, 0, 1], << size: 2 >>);

// 创建两条 3D 直线作为方向
line1 = view.create('line3d', [A, [0, 0, 1], [-Infinity, Infinity]], <<
    strokeColor: 'blue'
>>);
line2 = view.create('line3d', [A, [1, 1, 0], [-Infinity, Infinity]], <<
    strokeColor: 'blue'
>>);

// 通过点和两条直线创建平面
plane = view.create('plane3d', [A, line1, line2], <<
    fillColor: 'blue'
>>);
```

### 4. 通过三个点创建平面

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]], <<
    depthOrder: << enabled: true >>,
    projection: 'central'
>>);

// 创建三个点
A = view.create('point3d', [0, 0, 1], << size: 2 >>);
B = view.create('point3d', [2, 2, 1], << size: 2 >>);
C = view.create('point3d', [-2, 0, 1], << size: 2 >>);

// 通过三个点创建平面
plane = view.create('plane3d', [A, B, C], <<
    fillColor: 'blue'
>>);
```

### 5. 简化语法（省略范围）

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]], <<
    depthOrder: << enabled: true >>,
    projection: 'central'
>>);

A = view.create('point3d', [-2, 0, 1], << size: 2 >>);

// 无限平面，range1 = range2 = [-Infinity, Infinity]（默认）
plane1 = view.create('plane3d', [A, [1, 0, 0], [0, 1, 0]], <<
    fillColor: 'blue'
>>);

// 使用 threePoints 选项，将第二、三参数解释为点
plane2 = view.create('plane3d', [A, [1, 0, 0], [0, 1, 0]], <<
    threePoints: true,
    fillColor: 'red',
    point2: << visible: true >>,
    point3: << visible: true >>
>>);
```

### 6. 动态平面

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]]);

// 创建滑块
t = slider(0, 2*PI, 0.01);

// 创建一个随滑块移动的点
P = view.create('point3d', [
    () => cos(V(t)),
    () => sin(V(t)),
    0
], << size: 3 >>);

// 平面随点移动
plane = view.create('plane3d', [
    P,
    [1, 0, 0],
    [0, 1, 0],
    [-2, 2],
    [-2, 2]
], << fillOpacity: 0.5 >>);
```

## 注意事项

1. **线性无关**：两个方向向量必须是线性无关的，否则无法定义平面
2. **无限与有限**：如果范围为 [-Infinity, Infinity] 或未指定，平面将无限延伸；否则为有限平面
3. **网格**：有限平面可以显示网格（mesh3d），无限平面不支持
4. **三点方式**：使用 `threePoints: true` 属性可以将第二、三参数解释为点坐标而非方向向量
5. **3D 视图**：3D 平面必须在 3D 视图（view3d）中创建和显示

## 相关元素

- [Point3D](./Point3D.md) - 3D 点
- [Line3D](./Line3D.md) - 3D 直线
- [Mesh3D](./Mesh3D.md) - 3D 网格
- [View3D](./View3D.md) - 3D 视图
