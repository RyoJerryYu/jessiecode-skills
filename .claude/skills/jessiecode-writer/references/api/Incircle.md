# Incircle 内切圆

## 描述

内切圆是与三角形的三条边都相切的圆。内切圆由三角形的三个顶点定义，圆心是三角形的内心（三条角平分线的交点）。

## JessieCode 语法

```js
// 基本语法 - 通过三角形的三个顶点创建内切圆
incircle = incircle(p1, p2, p3);

// 带属性创建
incircle = incircle(A, B, C) <<
    strokeColor: 'red',
    strokeWidth: 2,
    dash: 1
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| p1 | Point | 三角形的第一个顶点 |
| p2 | Point | 三角形的第二个顶点 |
| p3 | Point | 三角形的第三个顶点 |

**注意**：三个点不能共线，否则无法构成三角形。

## 属性

内切圆继承自 Circle，拥有圆的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `fillOpacity` | Number | 0.0 | 填充透明度 (0-1) |
| `dash` | Number | 0 | 虚线样式 |
| `opacity` | Number | 1.0 | 透明度 |
| `visible` | Boolean | true | 是否可见 |
| `center` | Object | - | 圆心属性设置 |

### 圆心属性

```js
// 显示内切圆圆心（内心）
incircle = incircle(A, B, C) <<
    center: <<
        visible: true,
        strokeColor: 'red',
        size: 5
    >>
>>;
```

## 方法

内切圆继承自 Circle，拥有圆的所有方法：

| 方法 | 参数 | 描述 |
|------|------|------|
| `Radius()` | 无 | 获取半径（内切圆半径） |
| `X()` | 无 | 获取圆心 x 坐标 |
| `Y()` | 无 | 获取圆心 y 坐标 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `radius(incircle)` | 获取内切圆半径 | `radius(incircle)` |
| `area(incircle)` | 获取内切圆面积 | `area(incircle)` |
| `perimeter(incircle)` | 获取内切圆周长 | `perimeter(incircle)` |

## 示例

### 1. 创建基本内切圆

```js
// 三角形的三个顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 创建内切圆
incircle = incircle(A, B, C);

// 设置样式
incircle = incircle(A, B, C) <<
    strokeColor: 'red',
    strokeWidth: 2,
    dash: 1
>>;
```

### 2. 显示内心（内切圆圆心）

```js
// 三角形的三个顶点
A = point(0, 0);
B = point(4, 0);
C = point(1, 3);

// 内切圆，显示圆心
incircle = incircle(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    center: <<
        visible: true,
        strokeColor: 'red',
        fillColor: 'black',
        size: 5,
        withLabel: true,
        name: 'I'
    >>
>>;
```

### 3. 内切圆与三角形

```js
// 三角形的三个顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 三角形
tri = polygon(A, B, C) <<
    fillColor: 'lightgray',
    fillOpacity: 0.3,
    strokeColor: 'black',
    strokeWidth: 2
>>;

// 内切圆
incircle = incircle(A, B, C) <<
    strokeColor: 'red',
    strokeWidth: 2,
    fillOpacity: 0
>>;

// 内心
I = incenter(A, B, C) <<
    strokeColor: 'red',
    size: 5
>>;
```

### 4. 动态内切圆

```js
// 可移动的顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 内切圆随三角形变化
incircle = incircle(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 三角形
tri = polygon(A, B, C) <<
    fillColor: 'lightyellow',
    fillOpacity: 0.3
>>;

// 显示内切圆半径
radiusText = text(-3, 4, function() {
    return "Radius: " + incircle.Radius().toFixed(3);
});

// 显示内切圆面积
areaText = text(-3, 3.5, function() {
    return "Area: " + area(incircle).toFixed(3);
});
```

### 5. 内切圆半径与三角形面积的关系

```js
// 三角形的三个顶点
A = point(0, 0);
B = point(4, 0);
C = point(1, 3);

// 三角形
tri = polygon(A, B, C) <<
    fillColor: 'lightblue',
    fillOpacity: 0.3
>>;

// 内切圆
incircle = incircle(A, B, C) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

// 内心
I = incenter(A, B, C) <<
    strokeColor: 'red',
    size: 5
>>;

// 内切圆半径
r = incircle.Radius();

// 三角形周长
perimeter = dist(A, B) + dist(B, C) + dist(C, A);

// 三角形面积 = r * s (s 为半周长)
s = perimeter / 2;
calculatedArea = r * s;

// 显示关系
relationText = text(-4, 4, function() {
    r = incircle.Radius();
    p = dist(A, B) + dist(B, C) + dist(C, A);
    s = p / 2;
    return "Area = r × s = " + (r * s).toFixed(3);
});
```

### 6. 内切圆与三边的切点

```js
// 三角形的三个顶点
A = point(0, 0);
B = point(4, 0);
C = point(1, 3);

// 内切圆
incircle = incircle(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 内心
I = incenter(A, B, C) <<
    strokeColor: 'red',
    size: 5
>>;

// 内切圆与三边的切点（垂足）
footAB = perpendicularpoint(I, line(A, B)) <<
    strokeColor: 'green',
    size: 4
>>;
footBC = perpendicularpoint(I, line(B, C)) <<
    strokeColor: 'green',
    size: 4
>>;
footCA = perpendicularpoint(I, line(C, A)) <<
    strokeColor: 'green',
    size: 4
>>;

// 连接内心与切点
r1 = segment(I, footAB) << strokeColor: 'gray', dash: 1 >>;
r2 = segment(I, footBC) << strokeColor: 'gray', dash: 1 >>;
r3 = segment(I, footCA) << strokeColor: 'gray', dash: 1 >>;
```

### 7. 特殊三角形的内切圆

```js
// 等边三角形
A1 = point(0, 0);
B1 = point(4, 0);
C1 = point(2, 2 * sqrt(3));
tri1 = polygon(A1, B1, C1) <<
    fillColor: 'lightblue',
    fillOpacity: 0.3
>>;
incircle1 = incircle(A1, B1, C1) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

// 等腰三角形
A2 = point(6, 0);
B2 = point(10, 0);
C2 = point(8, 4);
tri2 = polygon(A2, B2, C2) <<
    fillColor: 'lightgreen',
    fillOpacity: 0.3
>>;
incircle2 = incircle(A2, B2, C2) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 直角三角形
A3 = point(0, -5);
B3 = point(3, -5);
C3 = point(0, -2);
tri3 = polygon(A3, B3, C3) <<
    fillColor: 'lightyellow',
    fillOpacity: 0.3
>>;
incircle3 = incircle(A3, B3, C3) <<
    strokeColor: 'orange',
    strokeWidth: 2
>>;
```

### 8. 内切圆与外接圆对比

```js
// 三角形的三个顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 三角形
tri = polygon(A, B, C) <<
    fillColor: 'lightgray',
    fillOpacity: 0.3
>>;

// 内切圆
incircle = incircle(A, B, C) <<
    strokeColor: 'red',
    strokeWidth: 2,
    dash: 1
>>;

// 内心
I = incenter(A, B, C) <<
    strokeColor: 'red',
    size: 5,
    withLabel: true,
    name: 'I'
>>;

// 外接圆（使用 circumcircle 创建）
circumcircle = circumcircle(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    dash: 1
>>;

// 外心
O = circumcenter(A, B, C) <<
    strokeColor: 'blue',
    size: 5,
    withLabel: true,
    name: 'O'
>>;

// 显示两个圆的关系
relationText = text(-4, 5, "Red: Incircle, Blue: Circumcircle");
```

### 9. 内切圆的欧拉公式

```js
// 三角形的三个顶点
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

// 三角形
tri = polygon(A, B, C) <<
    fillColor: 'lightgray',
    fillOpacity: 0.3
>>;

// 内切圆和外接圆
incircle = incircle(A, B, C) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;
circumcircle = circumcircle(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 内心和外心
I = incenter(A, B, C) << strokeColor: 'red', size: 5 >>;
O = circumcenter(A, B, C) << strokeColor: 'blue', size: 5 >>;

// 欧拉公式：d² = R(R-2r)
// d 是内心和外心的距离
// R 是外接圆半径，r 是内切圆半径
eulerText = text(-4, 5, function() {
    d = dist(I, O);
    R = circumcircle.Radius();
    r = incircle.Radius();
    lhs = d * d;
    rhs = R * (R - 2 * r);
    return "d²=" + lhs.toFixed(3) + ", R(R-2r)=" + rhs.toFixed(3);
});
```

### 10. 内切圆半径公式演示

```js
// 直角三角形（内切圆半径公式最简单）
A = point(0, 0);
B = point(4, 0);
C = point(0, 3);

// 三角形
tri = polygon(A, B, C) <<
    fillColor: 'lightyellow',
    fillOpacity: 0.3
>>;

// 内切圆
incircle = incircle(A, B, C) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

// 直角三角形的内切圆半径公式：r = (a + b - c) / 2
// 其中 c 是斜边
r_formula = (dist(A, B) + dist(A, C) - dist(B, C)) / 2;

// 显示公式
formulaText = text(-4, 4, function() {
    a = dist(B, C);
    b = dist(A, C);
    c = dist(A, B);
    r = incircle.Radius();
    calculated = (b + c - a) / 2;  // 根据实际边长调整
    return "r = (a+b-c)/2 = " + calculated.toFixed(3);
});
```

## 注意事项

1. **三点不共线**：三个顶点不能共线，否则无法构成三角形
2. **内心位置**：内切圆圆心（内心）始终在三角形内部
3. **相切性质**：内切圆与三角形三边都相切
4. **半径计算**：内切圆半径 = 三角形面积 / 半周长
5. **唯一性**：每个三角形有且仅有一个内切圆

## 相关元素

- [Incenter](./Incenter.md) - 内心
- [Circumcircle](./Circumcircle.md) - 外接圆
- [Circle](./Circle.md) - 圆
- [Polygon](./Polygon.md) - 多边形
