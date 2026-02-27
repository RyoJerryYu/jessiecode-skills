# Polygon 多边形

## 描述

多边形是由线段（边）连接顶点形成的封闭平面图形。顶点按顺序连接，最后一个顶点会自动与第一个顶点连接形成封闭图形。

## JessieCode 语法

```js
// 通过三个或更多点创建多边形
pol = polygon(A, B, C);

// 通过点数组创建
pol = polygon(A, B, C, D, E);

// 带属性创建
pol = polygon(A, B, C) <<
    fillColor: 'yellow',
    fillOpacity: 0.3,
    borders: <<
        strokeWidth: 2,
        strokeColor: 'blue'
    >>
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| vertices | Point/Array/Function | 多边形的顶点（至少 3 个） |

顶点可以是：
- `JXG.Point` 对象
- 坐标数组 `[x, y]`
- 返回坐标的函数

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `fillColor` | String | '#ffff00' | 填充颜色 |
| `fillOpacity` | Number | 0.8 | 填充透明度 (0-1) |
| `opacity` | Number | 1.0 | 整体透明度 |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 多边形名称 |
| `borders` | Object | - | 边的属性设置 |
| `vertices` | Object | - | 顶点的属性设置 |
| `hasInnerPoints` | Boolean | false | 内部点是否触发交互 |
| `highlightByStrokeWidth` | Boolean | false | 高亮时是否改变边宽 |

### 边的属性

```js
pol = polygon(A, B, C) <<
    borders: <<
        strokeWidth: 2,
        strokeColor: 'red',
        dash: 1
    >>
>>;
```

### 顶点的属性

```js
pol = polygon(A, B, C) <<
    vertices: <<
        visible: true,
        strokeColor: 'blue',
        size: 4,
        withLabel: true
    >>
>>;
```

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `area()` | 无 | 获取多边形面积 |
| `L()` | 无 | 获取多边形周长 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `area(polygon)` | 获取多边形面积 | `area(pol)` |
| `perimeter(polygon)` | 获取多边形周长 | `perimeter(pol)` |

## 示例

### 1. 创建基本多边形

```js
// 三角形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);
tri = polygon(A, B, C);

// 四边形
D = point(-2, -2);
E = point(2, -2);
F = point(2, 2);
G = point(-2, 2);
quad = polygon(D, E, F, G);

// 五边形
pol5 = polygon(A, B, C, D, E);
```

### 2. 设置多边形样式

```js
// 黄色填充的三角形
tri1 = polygon(A, B, C) <<
    fillColor: 'yellow',
    fillOpacity: 0.5
>>;

// 半透明蓝色四边形
quad1 = polygon(D, E, F, G) <<
    fillColor: 'blue',
    fillOpacity: 0.2,
    strokeColor: 'darkblue',
    strokeWidth: 2
>>;

// 仅边框，无填充
tri2 = polygon(A, B, C) <<
    fillColor: 'none',
    strokeColor: 'red',
    strokeWidth: 3
>>;
```

### 3. 设置边的样式

```js
// 虚线边框
pol = polygon(A, B, C, D) <<
    borders: <<
        strokeWidth: 2,
        strokeColor: 'blue',
        dash: 1
    >>
>>;

// 每条边不同颜色（通过 borders 数组索引）
pol2 = polygon(E, F, G, H) <<
    borders: <<
        strokeWidth: 3
    >>
>>;
pol2.borders[0].strokeColor = 'red';
pol2.borders[1].strokeColor = 'green';
pol2.borders[2].strokeColor = 'blue';
pol2.borders[3].strokeColor = 'orange';
```

### 4. 设置顶点样式

```js
// 显示顶点
pol = polygon(A, B, C) <<
    vertices: <<
        visible: true,
        strokeColor: 'red',
        fillColor: 'black',
        size: 5,
        face: '[]'
    >>
>>;

// 显示顶点标签
pol2 = polygon(D, E, F) <<
    vertices: <<
        visible: true,
        withLabel: true
    >>
>>;
```

### 5. 三角形类型

```js
// 等边三角形
A = point(0, 0);
B = point(4, 0);
C = point(2, 2 * sqrt(3));
equilateral = polygon(A, B, C) << fillColor: 'lightgreen' >>;

// 等腰三角形
D = point(-2, 0);
E = point(2, 0);
F = point(0, 4);
isosceles = polygon(D, E, F) << fillColor: 'lightblue' >>;

// 直角三角形
G = point(0, 0);
H = point(3, 0);
I = point(0, 4);
right = polygon(G, H, I) << fillColor: 'lightyellow' >>;
```

### 6. 正多边形

```js
// 正六边形（使用循环）
O = point(0, 0);
n = 6;
r = 2;

// 创建顶点
for (i = 0; i < n; i = i + 1) {
    angle = 2 * PI * i / n;
    px = r * cos(angle);
    py = r * sin(angle);
    // 存储顶点
}

// 更简单的方式：直接使用 RegularPolygon
// 见 RegularPolygon 文档
```

### 7. 获取多边形属性

```js
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);
pol = polygon(A, B, C);

// 使用全局函数
a = area(pol);      // 面积
p = perimeter(pol); // 周长

// 使用元素方法
a2 = pol.area();
p2 = pol.L();

// 获取边
border0 = pol.borders[0];  // 第一条边 AB
border1 = pol.borders[1];  // 第二条边 BC
border2 = pol.borders[2];  // 第三条边 CA

// 获取顶点
vertex0 = pol.vertices[0];  // 顶点 A
```

### 8. 动态多边形

```js
// 创建可拖动的顶点
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);

// 多边形
pol = polygon(A, B, C) <<
    fillColor: 'yellow',
    fillOpacity: 0.5
>>;

// 显示面积和周长
areaText = text(-2, 3, "Area: " + area(pol));
perimeterText = text(-2, 2.5, "Perimeter: " + perimeter(pol));

// 拖动顶点时，面积和周长会实时更新
```

### 9. 嵌套多边形

```js
// 外三角形
A = point(-3, -2);
B = point(3, -2);
C = point(0, 3);
outer = polygon(A, B, C) << fillColor: 'lightblue' >>;

// 中点三角形
mAB = midpoint(A, B);
mBC = midpoint(B, C);
mCA = midpoint(C, A);
inner = polygon(mAB, mBC, mCA) << fillColor: 'lightgreen' >>;
```

### 10. 使用坐标数组创建多边形

```js
// 直接使用坐标
pol = polygon(
    point(0, 0),
    point(2, 0),
    point(2, 2),
    point(0, 2)
) << fillColor: 'pink' >>;

// 或使用函数返回坐标
f1 = function() { return [0, 0]; };
f2 = function() { return [2, 0]; };
f3 = function() { return [2, 2]; };
f4 = function() { return [0, 2]; };
pol2 = polygon(f1(), f2(), f3(), f4());
```

### 11. 多边形与变换

```js
// 原多边形
A = point(-2, -1);
B = point(0, 2);
C = point(2, -1);
pol1 = polygon(A, B, C) << fillColor: 'blue' >>;

// 创建缩放变换
scale = transform(2, 2) << type: 'scale' >>;

// 变换后的多边形
pol2 = polygon(pol1, scale) << fillColor: 'red', fillOpacity: 0.3 >>;
```

## 注意事项

1. **封闭图形**：多边形自动封闭，最后一个顶点会连接到第一个顶点
2. **顶点顺序**：顶点应按顺时针或逆时针顺序给出，影响面积的正负
3. **边数组**：`pol.borders[i]` 可以访问第 i 条边
4. **顶点数组**：`pol.vertices[i]` 可以访问第 i 个顶点
5. **自相交**：避免创建自相交的多边形，可能导致填充异常

## 相关元素

- [RegularPolygon](./RegularPolygon.md) - 正多边形
- [Triangle](./Triangle.md) - 三角形
- [Quadrangle](./Quadrangle.md) - 四边形
- [Segment](./Segment.md) - 线段（多边形的边）
