# Parallelogram 平行四边形

## 描述

平行四边形是一种四边形，其对边相互平行。

*定义于：* [polygon.js](./src/src_base_polygon.js.md)
*继承自：* [Polygon](./Polygon.md)

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
&nbsp;&nbsp;&nbsp;↳ **[JXG.Polygon](./JXG.Polygon.md)**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ **[Polygon](./Polygon.md)**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↳ **Parallelogram**

## JessieCode 语法

```js
// 通过三个点创建平行四边形
par = parallelogram(A, B, C);

// 带属性创建
par = parallelogram(A, B, C) <<
    hasInnerPoints: true,
    parallelpoint: <<
        size: 6,
        face: '<>'
    >>
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| p1 | Point/Array | 第一个顶点 |
| p2 | Point/Array | 第二个顶点 |
| p3 | Point/Array | 第三个顶点 |

**说明：** 平行四边形是通过点 [p1, p2, pp, p3] 形成的多边形，其中 pp 是第四个顶点（平行点），可作为子对象 `parallelogram.parallelPoint` 访问。

## 属性

平行四边形继承自 [Polygon](./Polygon.md)，因此具有多边形的所有属性。此外，它还有以下特殊属性：

| 属性 | 类型 | 描述 |
|------|------|------|
| `parallelPoint` | Point | 第四个顶点，使四边形成为平行四边形 |
| `hasInnerPoints` | Boolean | 内部点是否触发交互 |

### parallelPoint 属性

`parallelPoint` 是自动计算的第四个顶点，它使四边形成为平行四边形。也可以通过 `parallelogram.vertices[2]` 访问。

```js
// 设置 parallelPoint 的样式
par = parallelogram(A, B, C) <<
    parallelpoint: <<
        size: 6,
        face: '<>',
        strokeColor: 'red',
        withLabel: true
    >>
>>;
```

## 方法

平行四边形继承自 [Polygon](./Polygon.md)，因此具有多边形的所有方法：

| 方法 | 参数 | 描述 |
|------|------|------|
| `area()` | 无 | 获取平行四边形面积 |
| `L()` | 无 | 获取平行四边形周长 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `area(parallelogram)` | 获取平行四边形面积 | `area(par)` |
| `perimeter(parallelogram)` | 获取平行四边形周长 | `perimeter(par)` |

## 示例

### 1. 创建基本平行四边形

```js
// 创建三个顶点
A = point(-3, -4);
B = point(3, -1);
C = point(-2, 0);

// 创建平行四边形
par = parallelogram(A, B, C);
```

### 2. 设置平行四边形样式

```js
A = point(-3, -4);
B = point(3, -1);
C = point(-2, 0);

// 带填充色的平行四边形
par1 = parallelogram(A, B, C) <<
    fillColor: 'lightblue',
    fillOpacity: 0.5,
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 3. 显示第四个顶点

```js
A = point(-3, -4);
B = point(3, -1);
C = point(-2, 0);

// 显示平行点（第四个顶点）
par = parallelogram(A, B, C) <<
    hasInnerPoints: true,
    parallelpoint: <<
        size: 6,
        face: '<>',
        strokeColor: 'red',
        withLabel: true,
        name: 'D'
    >>
>>;
```

### 4. 访问平行点

```js
A = point(-3, -4);
B = point(3, -1);
C = point(-2, 0);

par = parallelogram(A, B, C);

// 方式一：使用 parallelPoint 属性
D1 = par.parallelPoint;

// 方式二：使用 vertices 数组（索引 2）
D2 = par.vertices[2];

// 获取平行点的坐标
dx = D1.X();
dy = D1.Y();
```

### 5. 动态平行四边形

```js
// 创建可拖动的顶点
A = point(-3, -4);
B = point(3, -1);
C = point(-2, 0);

// 创建平行四边形
par = parallelogram(A, B, C) <<
    fillColor: 'yellow',
    fillOpacity: 0.4
>>;

// 显示面积和周长
areaText = text(-4, 3, "Area: " + area(par));
perimeterText = text(-4, 2.5, "Perimeter: " + perimeter(par));

// 拖动顶点 A、B 或 C 时，平行四边形会自动更新
```

### 6. 平行四边形的边

```js
A = point(-3, -4);
B = point(3, -1);
C = point(-2, 0);

par = parallelogram(A, B, C);

// 访问边
side1 = par.borders[0];  // AB
side2 = par.borders[1];  // B 到平行点
side3 = par.borders[2];  // 平行点到 C
side4 = par.borders[3];  // CA

// 设置边的样式
side1.strokeColor = 'red';
side2.strokeColor = 'green';
side3.strokeColor = 'blue';
side4.strokeColor = 'orange';
```

### 7. 特殊的平行四边形

```js
// 矩形（特殊的平行四边形）
A = point(0, 0);
B = point(4, 0);
C = point(0, 3);
rect = parallelogram(A, B, C) <<
    fillColor: 'lightgreen'
>>;

// 菱形（特殊的平行四边形）
D = point(0, 0);
E = point(3, 2);
F = point(6, 0);
rhombus = parallelogram(D, E, F) <<
    fillColor: 'lightyellow'
>>;
```

### 8. 平行四边形与变换

```js
// 原平行四边形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);
par1 = parallelogram(A, B, C) << fillColor: 'blue' >>;

// 创建旋转变换
rotate = transform(0, 0) <<
    type: 'rotate',
    angle: 45
>>;

// 变换后的平行四边形
par2 = parallelogram(par1, rotate) <<
    fillColor: 'red',
    fillOpacity: 0.3
>>;
```

### 9. 使用坐标数组创建

```js
// 直接使用坐标数组
par = parallelogram(
    [-3, -4],
    [3, -1],
    [-2, 0]
) << fillColor: 'pink' >>;

// 或使用函数返回坐标
f1 = function() { return [-3, -4]; };
f2 = function() { return [3, -1]; };
f3 = function() { return [-2, 0]; };
par2 = parallelogram(f1(), f2(), f3());
```

### 10. 平行四边形的性质演示

```js
// 创建平行四边形
A = point(-3, -4);
B = point(3, -1);
C = point(-2, 0);
par = parallelogram(A, B, C) <<
    fillColor: 'lightblue',
    fillOpacity: 0.4
>>;

// 显示对边平行
side1 = par.borders[0];  // AB
side3 = par.borders[2];  // 对边

// 计算斜率（演示对边平行）
// 可以在文本中显示斜率值来验证平行
slope1 = text(-4, 4, "Slope AB: " + ...);
slope2 = text(-4, 3.5, "Slope opposite: " + ...);
```

## 注意事项

1. **三个点确定平行四边形**：给定三个点，第四个点（平行点）会自动计算，使得对边平行
2. **点的顺序**：点的顺序很重要，平行四边形通过 [p1, p2, parallelPoint, p3] 形成
3. **parallelPoint 访问**：可以通过 `parallelogram.parallelPoint` 或 `parallelogram.vertices[2]` 访问第四个顶点
4. **继承属性**：平行四边形继承自 Polygon，因此具有多边形的所有属性和方法
5. **hasInnerPoints**：设置 `hasInnerPoints: true` 可以让内部点触发交互事件

## 相关元素

- [Polygon](./Polygon.md) - 多边形（父类）
- [Rectangle](./Rectangle.md) - 矩形（特殊的平行四边形）
- [Rhombus](./Rhombus.md) - 菱形（特殊的平行四边形）
- [Square](./Square.md) - 正方形（特殊的平行四边形）
- [Quadrangle](./Quadrangle.md) - 四边形
- [Parallel](./Parallel.md) - 平行线
- [Vector](./Vector.md) - 向量（与平行四边形密切相关）
