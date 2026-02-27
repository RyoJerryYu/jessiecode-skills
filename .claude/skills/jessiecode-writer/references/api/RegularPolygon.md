# RegularPolygon 正多边形

<!-- USAGE_FREQUENCY: advanced -->

## 描述

正多边形是等角（所有角度量相等）且等边（所有边长相等）的多边形。它需要两个点来定义底边以及顶点的数量。

## JessieCode 语法

```js
// 通过两个点和顶点数创建正多边形
poly = regularpolygon(A, B, n);

// 通过三个点创建正多边形（第三个点决定顶点数）
poly = regularpolygon(A, B, C);

// 带属性创建
poly = regularpolygon(A, B, 5) <<
    fillColor: 'yellow',
    fillOpacity: 0.5,
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

## 参数

### 方式一：两个点 + 顶点数

| 参数 | 类型 | 描述 |
|------|------|------|
| point1 | Point/Array/Function | 第一个顶点 |
| point2 | Point/Array/Function | 第二个顶点（定义底边） |
| n | Number/Function | 顶点数量（正 n 边形） |

### 方式二：三个点

| 参数 | 类型 | 描述 |
|------|------|------|
| point1 | Point/Array/Function | 第一个顶点 |
| point2 | Point/Array/Function | 第二个顶点（定义底边） |
| point3 | Point/Array/Function | 第三个点，用于确定顶点数 |

**注意**：使用三个点时，顶点数由点 1 到点 2 的距离除以点 2 到点 3 的距离确定

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `fillColor` | String | '#FFFF00' | 填充颜色 |
| `fillOpacity` | Number | 0.3 | 填充透明度 (0-1) |
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 边线宽度（像素） |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线 |
| `opacity` | Number | 1.0 | 整体透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 多边形名称 |
| `withLines` | Boolean | true | 是否显示边框线 |
| `hasInnerPoints` | Boolean | false | 内部点是否触发 hasPoint |

### 顶点属性 (vertices)

```js
poly = regularpolygon(A, B, 5) <<
    vertices: <<
        strokeColor: 'red',
        fillColor: 'white',
        size: 4,
        withLabel: true
    >>
>>;
```

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | 继承 | 顶点描边颜色 |
| `fillColor` | String | 继承 | 顶点填充颜色 |
| `size` | Number | 继承 | 顶点大小 |
| `withLabel` | Boolean | false | 是否显示顶点标签 |
| `name` | String | 自动生成 | 顶点命名格式 |

### 边框属性 (borders)

```js
poly = regularpolygon(A, B, 5) <<
    borders: <<
        strokeColor: 'blue',
        strokeWidth: 2,
        dash: 1
    >>
>>;
```

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | 继承 | 边框颜色 |
| `strokeWidth` | Number | 继承 | 边框宽度 |
| `dash` | Number | 继承 | 边框虚线样式 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `getVertex(i)` | i: Number | 获取第 i 个顶点 |
| `getVertexNumber()` | 无 | 获取顶点数量 |
| `getPolynomial()` | 无 | 获取面积多项式 |
| `area()` | 无 | 计算多边形面积 |
| `hasPoint(x, y)` | x, y: Number | 判断点是否在多边形内 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `Area(poly)` | 计算多边形面积 | `Area(poly)` |

## 示例

### 1. 创建基本正多边形

```js
// 创建两个点定义底边
A = point(0, 0);
B = point(3, 0);

// 创建正五边形
poly5 = regularpolygon(A, B, 5);

// 创建正六边形
poly6 = regularpolygon(A, B, 6);

// 创建正三角形（等边三角形）
poly3 = regularpolygon(A, B, 3);
```

### 2. 创建正方形

```js
// 通过两个相邻顶点创建正方形
A = point(1, 1);
B = point(4, 1);

// 正四边形即正方形
square = regularpolygon(A, B, 4);
```

### 3. 设置样式

```js
// 黄色填充的正五边形
poly1 = regularpolygon(A, B, 5) <<
    fillColor: 'yellow',
    fillOpacity: 0.6,
    strokeColor: 'orange',
    strokeWidth: 3
>>;

// 半透明蓝色正六边形
poly2 = regularpolygon(C, D, 6) <<
    fillColor: 'blue',
    fillOpacity: 0.3,
    strokeColor: 'darkblue'
>>;

// 虚线边框的正三角形
poly3 = regularpolygon(E, F, 3) <<
    fillOpacity: 0.5,
    strokeColor: 'green',
    dash: 1
>>;
```

### 4. 带顶点标签的正多边形

```js
// 显示顶点标签
poly = regularpolygon(A, B, 5) <<
    vertices: <<
        withLabel: true,
        strokeColor: 'red',
        fillColor: 'white',
        size: 5
    >>,
    fillOpacity: 0.3
>>;
```

### 5. 通过三个点创建

```js
// 第三个点用于确定顶点数
A = point(0, 0);
B = point(4, 0);
C = point(4, 1);  // BC 距离决定边数

// 根据 AB/BC 的比例确定顶点数
poly = regularpolygon(A, B, C);
```

### 6. 动态正多边形

```js
// 创建滑块控制边数
n = slider(3, 12, 1);

// 固定点
A = point(-2, 0) << fixed: true >>;
B = point(2, 0) << fixed: true >>;

// 边数可变的正多边形
poly = regularpolygon(A, B, n);

// 显示当前边数
text = text(0, 3, function() {
    return "边数：" + Math.round(V(n));
});
```

### 7. 正多边形变换

```js
// 创建正五边形
A = point(0, 0);
B = point(2, 0);
poly1 = regularpolygon(A, B, 5);

// 创建旋转中心
O = point(0, 0) << fixed: true >>;

// 创建旋转变换
rot = transform(O) << type: 'rotate', angle: PI/5 >>;

// 旋转后的正五边形
poly2 = regularpolygon(poly1, rot);
```

### 8. 计算面积

```js
// 创建正六边形
A = point(0, 0);
B = point(3, 0);
hex = regularpolygon(A, B, 6);

// 计算面积
area = Area(hex);

// 或使用元素方法
area2 = hex.area();

// 显示面积
text = text(1, -1, function() {
    return "面积：" + Math.round(V(area) * 100) / 100;
});
```

### 9. 嵌套正多边形

```js
// 外层正五边形
A = point(0, 0);
B = point(4, 0);
poly1 = regularpolygon(A, B, 5) <<
    fillColor: 'lightblue',
    fillOpacity: 0.5
>>;

// 获取顶点创建内层多边形
C = poly1.getVertex(0);
D = poly1.getVertex(1);
poly2 = regularpolygon(C, D, 5) <<
    fillColor: 'lightgreen',
    fillOpacity: 0.5
>>;
```

### 10. 正多边形序列

```js
// 创建一系列正多边形展示逼近圆的效果
O = point(0, 0) << fixed: true >>;
R = point(3, 0) << fixed: true >>;

// 正三角形
poly3 = regularpolygon(O, R, 3) << fillOpacity: 0.1 >>;

// 正方形
poly4 = regularpolygon(O, R, 4) << fillOpacity: 0.1 >>;

// 正六边形
poly6 = regularpolygon(O, R, 6) << fillOpacity: 0.1 >>;

// 正十二边形（接近圆）
poly12 = regularpolygon(O, R, 12) << fillOpacity: 0.1 >>;
```

## 注意事项

1. **顶点数限制**：正多边形的顶点数必须大于等于 3
2. **方向**：正多边形默认按逆时针方向构建
3. **顶点访问**：使用 `getVertex(i)` 方法访问第 i 个顶点（从 0 开始计数）
4. **动态边数**：使用滑块控制边数时，确保滑块步长为 1
5. **面积计算**：使用 `Area(poly)` 全局函数或 `poly.area()` 方法计算面积

## 相关元素

- [Polygon](./Polygon.md) - 多边形
- [Triangle](./Triangle.md) - 三角形
- [Square](./Square.md) - 正方形
- [Circle](./Circle.md) - 圆（正多边形的极限）
