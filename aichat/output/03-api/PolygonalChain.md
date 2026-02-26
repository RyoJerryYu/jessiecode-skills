# PolygonalChain 折线

## 描述

折线是一系列相连的线段（边）。它由顶点数组定义，顶点按顺序连接形成开放的路径。与多边形（Polygon）不同，折线不会自动封闭（最后一个顶点不会连接到第一个顶点）。

## JessieCode 语法

```js
// 通过两个或更多点创建折线
chain = polygonalchain(A, B, C);

// 通过点数组创建
chain = polygonalchain(A, B, C, D, E);

// 带属性创建
chain = polygonalchain(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 3,
    borders: <<
        strokeColor: 'red',
        strokeWidth: 2
    >>
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| vertices | Point/Array/Function | 折线的顶点（至少 2 个） |

顶点可以是：
- `JXG.Point` 对象
- 坐标数组 `[x, y]`
- 返回坐标的函数

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式 |
| `opacity` | Number | 1.0 | 透明度 |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 折线名称 |
| `borders` | Object | - | 边的属性设置 |
| `vertices` | Object | - | 顶点的属性设置 |
| `highlightStrokeWidth` | Number | - | 高亮时的线宽 |

### 边的属性

```js
// 设置所有边的统一样式
chain = polygonalchain(A, B, C, D) <<
    borders: <<
        strokeWidth: 3,
        strokeColor: 'blue',
        dash: 2
    >>
>>;
```

### 顶点的属性

```js
// 显示顶点
chain = polygonalchain(A, B, C) <<
    vertices: <<
        visible: true,
        strokeColor: 'red',
        fillColor: 'black',
        size: 4
    >>
>>;
```

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `L()` | 无 | 获取折线总长度 |

## 示例

### 1. 创建基本折线

```js
// 通过三个点创建折线
A = point(-2, 0);
B = point(0, 2);
C = point(2, 0);
chain = polygonalchain(A, B, C);

// 通过更多点创建复杂折线
D = point(-4, 0);
E = point(-2, -2);
F = point(0, 0);
G = point(2, -2);
H = point(4, 0);
chain2 = polygonalchain(D, E, F, G, H);
```

### 2. 设置折线样式

```js
// 红色粗折线
chain1 = polygonalchain(A, B, C) <<
    strokeColor: 'red',
    strokeWidth: 4
>>;

// 虚线折线
chain2 = polygonalchain(D, E, F) <<
    dash: 1,
    strokeColor: 'gray',
    strokeWidth: 2
>>;

// 蓝色折线
chain3 = polygonalchain(G, H, I) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;
```

### 3. 设置边的样式

```js
// 统一设置所有边的样式
chain = polygonalchain(A, B, C, D) <<
    borders: <<
        strokeWidth: 3,
        strokeColor: 'blue'
    >>
>>;

// 访问单独的边
chain = polygonalchain(E, F, G, H);
chain.borders[0].strokeColor = 'red';    // 第一条边
chain.borders[1].strokeColor = 'green';  // 第二条边
chain.borders[2].strokeColor = 'blue';   // 第三条边
```

### 4. 设置顶点样式

```js
// 显示顶点
chain = polygonalchain(A, B, C, D) <<
    vertices: <<
        visible: true,
        strokeColor: 'red',
        fillColor: 'black',
        size: 5,
        face: 'circle'
    >>
>>;

// 显示顶点标签
chain2 = polygonalchain(E, F, G) <<
    vertices: <<
        visible: true,
        withLabel: true
    >>
>>;
```

### 5. 使用坐标创建折线

```js
// 直接使用坐标数组
chain = polygonalchain(
    point(-3, 0),
    point(-1, 2),
    point(1, 0),
    point(3, 2)
);

// 或使用函数返回坐标
f1 = function() { return [-2, 0]; };
f2 = function() { return [0, 2]; };
f3 = function() { return [2, 0]; };
chain2 = polygonalchain(f1(), f2(), f3());
```

### 6. 动态折线

```js
// 创建可拖动的顶点
A = point(-2, 0);
B = point(0, 2);
C = point(2, 0);
D = point(4, 2);

// 折线
chain = polygonalchain(A, B, C, D) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 显示总长度
lenText = text(-3, 3, "Total length: " + L(chain));

// 拖动顶点时，折线形状和长度会实时更新
```

### 7. 获取折线属性

```js
A = point(-2, 0);
B = point(0, 2);
C = point(2, 0);
D = point(4, 2);
chain = polygonalchain(A, B, C, D);

// 获取总长度
totalLen = L(chain);

// 获取边的数量
numBorders = chain.borders.length;  // 3

// 获取顶点的数量
numVertices = chain.vertices.length;  // 4

// 访问单独的边
firstBorder = chain.borders[0];   // 边 AB
secondBorder = chain.borders[1];  // 边 BC

// 访问单独的顶点
firstVertex = chain.vertices[0];  // 顶点 A
```

### 8. 折线与多边形对比

```js
// 相同的顶点
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);

// 折线 - 开放路径
chain = polygonalchain(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 多边形 - 封闭图形
poly = polygon(A, B, C) <<
    fillColor: 'yellow',
    fillOpacity: 0.5
>>;

// 区别：多边形会自动封闭（C 连接回 A），折线不会
```

### 9. 折线与变换

```js
// 原折线
A = point(-2, 0);
B = point(0, 2);
C = point(2, 0);
chain1 = polygonalchain(A, B, C) << strokeColor: 'blue' >>;

// 创建平移变换
translate = transform(3, 1) << type: 'translate' >>;

// 变换后的折线（通过变换顶点实现）
A2 = transform(A, translate);
B2 = transform(B, translate);
C2 = transform(C, translate);
chain2 = polygonalchain(A2, B2, C2) <<
    strokeColor: 'red',
    strokeOpacity: 0.5
>>;
```

### 10. 折线路径动画

```js
// 创建滑块控制动画
t = slider(0, 2*PI, 0.01);

// 创建沿路径运动的点
// 使用参数方程定义路径上的点
path = polygonalchain(
    point(-3, 0),
    point(-1, 2),
    point(1, 0),
    point(3, 2)
);

// 点 P 沿折线运动（简化示例：在两点间运动）
P = point(
    function() { return -3 + 6 * (V(t) / (2*PI)); },
    function() { return sin(V(t)); }
) << size: 5, fillColor: 'red' >>;
```

### 11. 吸附到网格的折线

```js
// 创建带吸附功能的顶点
attr = << snapToGrid: true >>;

p1 = point(-4, 0, attr);
p2 = point(-2, -2, attr);
p3 = point(0, 0, attr);
p4 = point(2, -2, attr);
p5 = point(4, 0, attr);

// 创建折线
chain = polygonalchain(p1, p2, p3, p4, p5) <<
    strokeColor: 'blue',
    strokeWidth: 3,
    vertices: <<
        visible: true,
        size: 6
    >>
>>;
```

### 12. 心电图折线示例

```js
// 模拟心电图波形
x1 = point(-5, 0);
x2 = point(-4, 0);
x3 = point(-3, 0.5);   // 小上升
x4 = point(-2.5, 0);   // 回到基线
x5 = point(-2, 0);
x6 = point(-1.5, -0.3); // Q 波
x7 = point(-1, 1.5);    // R 波（高峰）
x8 = point(-0.5, -0.3); // S 波
x9 = point(0, 0);       // 回到基线
x10 = point(1, 0);
x11 = point(2, 0.3);    // T 波
x12 = point(3, 0);
x13 = point(5, 0);

// 创建心电图折线
ecg = polygonalchain(
    x1, x2, x3, x4, x5, x6, x7, x8, x9, x10, x11, x12, x13
) <<
    strokeColor: 'green',
    strokeWidth: 2
>>;
```

## 注意事项

1. **开放路径**：折线不会自动封闭，最后一个顶点不会连接到第一个顶点（与多边形不同）
2. **至少两个顶点**：创建折线至少需要两个顶点
3. **边的数组**：`chain.borders[i]` 可以访问第 i 条边
4. **顶点的数组**：`chain.vertices[i]` 可以访问第 i 个顶点
5. **长度计算**：`L(chain)` 返回所有边长度的总和
6. **与 Polygon 的区别**：Polygon 是封闭图形有填充区域，PolygonalChain 是开放路径只有边框

## 相关元素

- [Polygon](./Polygon.md) - 多边形（封闭图形）
- [Line](./Line.md) - 直线
- [Segment](./Segment.md) - 线段
- [Curve](./Curve.md) - 曲线
- [CardinalSpline](./Cardinalspline.md) - 基数样条曲线
