# Polygon3D 3D 多边形

<!-- USAGE_FREQUENCY: advanced -->

## 描述

3D 多边形是一系列按顺序连接的点，最后一个点与第一个点相连形成封闭图形。JSXGraph 不要求也不检查多边形是否共面。

## JessieCode 语法

```js
// 通过顶点数组创建 3D 多边形
polygon = polygon3d([A, B, C, D]);

// 带属性创建
polygon = polygon3d([A, B, C, D]) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    fillColor: 'yellow',
    fillOpacity: 0.3
>>;

// 在 3D 视图中创建
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]]);
polygon = view.create('polygon3d', [A, B, C, D]);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| vertices | Array | 3D 多边形的顶点数组，顶点可以是 Point3D 元素或坐标数组 |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 2 | 描边宽度 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `fillOpacity` | Number | 0.1 | 填充透明度 |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |

## 示例

### 1. 创建基本 3D 三角形

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]], <<
    depthOrder: << enabled: true >>,
    projection: 'central'
>>);

// 创建三个 3D 点
A = view.create('point3d', [0, 0, 0], << name: 'A' >>);
B = view.create('point3d', [2, 0, 0], << name: 'B' >>);
C = view.create('point3d', [1, 2, 1], << name: 'C' >>);

// 创建 3D 三角形
triangle = view.create('polygon3d', [A, B, C], <<
    fillColor: 'blue',
    fillOpacity: 0.5
>>);
```

### 2. 创建 3D 四边形

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]], <<
    depthOrder: << enabled: true >>,
    projection: 'central'
>>);

// 创建正方形的四个顶点
A = view.create('point3d', [-1, -1, 0], << name: 'A' >>);
B = view.create('point3d', [1, -1, 0], << name: 'B' >>);
C = view.create('point3d', [1, 1, 0], << name: 'C' >>);
D = view.create('point3d', [-1, 1, 0], << name: 'D' >>);

// 创建 3D 四边形
square = view.create('polygon3d', [A, B, C, D], <<
    fillColor: 'green',
    fillOpacity: 0.4,
    strokeColor: 'darkgreen',
    strokeWidth: 2
>>);
```

### 3. 创建空间五边形

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]], <<
    depthOrder: << enabled: true >>,
    projection: 'central'
>>);

// 创建空间五边形的顶点（不共面）
A = view.create('point3d', [2, 0, 0], << name: 'A' >>);
B = view.create('point3d', [0, 2, 0], << name: 'B' >>);
C = view.create('point3d', [-2, 0, 0], << name: 'C' >>);
D = view.create('point3d', [0, -2, 0], << name: 'D' >>);
E = view.create('point3d', [0, 0, 2], << name: 'E' >>);

// 创建空间五边形
pentagon = view.create('polygon3d', [A, B, C, D, E], <<
    fillColor: 'yellow',
    fillOpacity: 0.5,
    strokeColor: 'orange',
    strokeWidth: 3
>>);
```

### 4. 使用坐标数组创建多边形

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]]);

// 直接使用坐标数组创建多边形（不创建 Point3D 元素）
triangle = view.create('polygon3d', [
    [0, 0, 0],
    [2, 0, 0],
    [1, 2, 0]
], <<
    fillColor: 'pink',
    fillOpacity: 0.6
>>);
```

### 5. 动态 3D 多边形

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]], <<
    depthOrder: << enabled: true >>,
    projection: 'central'
>>);

// 创建滑块
t = slider(0, 2*PI, 0.01, << name: '旋转' >>);

// 创建固定点
A = view.create('point3d', [2, 0, 0], << name: 'A' >>);

// 创建旋转点
B = view.create('point3d', [
    () => 2 * cos(V(t)),
    () => 2 * sin(V(t)),
    0
], << name: 'B' >>);

C = view.create('point3d', [0, 0, 2], << name: 'C' >>);

// 创建动态三角形
triangle = view.create('polygon3d', [A, B, C], <<
    fillColor: 'cyan',
    fillOpacity: 0.5
>>);
```

### 6. 创建六边形

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]], <<
    depthOrder: << enabled: true >>,
    projection: 'central'
>>);

// 创建六边形的顶点（在 xy 平面上）
vertices = [];
for (i = 0; i < 6; i++) {
    angle = i * PI / 3;
    vertices[i] = view.create('point3d', [
        2 * cos(angle),
        2 * sin(angle),
        0
    ], << withLabel: false >>);
}

// 创建六边形
hexagon = view.create('polygon3d', vertices, <<
    fillColor: 'violet',
    fillOpacity: 0.4,
    strokeColor: 'purple',
    strokeWidth: 2
>>);
```

### 7. 多边形边框样式

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]]);

A = view.create('point3d', [-1, -1, 0]);
B = view.create('point3d', [1, -1, 0]);
C = view.create('point3d', [1, 1, 1]);
D = view.create('point3d', [-1, 1, 1]);

// 带虚线边框的多边形
quad = view.create('polygon3d', [A, B, C, D], <<
    fillColor: 'lightblue',
    fillOpacity: 0.5,
    strokeColor: 'navy',
    strokeWidth: 3
>>);
```

### 8. 嵌套多边形

```js
view = view3d([-6, -3], [8, 8], [[-3, 3], [-3, 3], [-3, 3]], <<
    depthOrder: << enabled: true >>,
    projection: 'central'
>>);

// 外层三角形
A1 = view.create('point3d', [0, 2, 0], << name: 'A1' >>);
B1 = view.create('point3d', [-2, -1, 0], << name: 'B1' >>);
C1 = view.create('point3d', [2, -1, 0], << name: 'C1' >>);

outer = view.create('polygon3d', [A1, B1, C1], <<
    fillColor: 'blue',
    fillOpacity: 0.3
>>);

// 内层三角形（中点连接）
A2 = view.create('point3d', [0, 0.5, 0], << name: 'A2' >>);
B2 = view.create('point3d', [-1, -0.5, 0], << name: 'B2' >>);
C2 = view.create('point3d', [1, -0.5, 0], << name: 'C2' >>);

inner = view.create('polygon3d', [A2, B2, C2], <<
    fillColor: 'red',
    fillOpacity: 0.5
>>);
```

## 注意事项

1. **顶点顺序**：顶点按给定顺序连接，最后一个顶点会自动与第一个顶点相连
2. **非共面性**：3D 多边形的顶点不需要共面，JSXGraph 会渲染由顶点定义的空间多边形
3. **填充**：只有当多边形相对观察者朝向正确时才会填充，可能需要调整观察角度
4. **3D 视图**：3D 多边形必须在 3D 视图（view3d）中创建和显示
5. **深度排序**：建议启用 `depthOrder: { enabled: true }` 以获得正确的渲染效果

## 相关元素

- [Point3D](./Point3D.md) - 3D 点
- [Polyhedron3D](./Polyhedron3D.md) - 3D 多面体
- [Plane3D](./Plane3D.md) - 3D 平面
- [View3D](./View3D.md) - 3D 视图
