# OtherIntersection 另一交点

<!-- USAGE_FREQUENCY: advanced -->

## 描述

当两个几何元素（如曲线、圆或直线）有多个交点时，可以使用此元素创建"另一个"交点。

**继承自：** [JXG.Point](./Point.md)
**定义于：** [point.js](./src/src_base_point.js.md)

## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md), JXG.GeometryElement**
   ↳ **[JXG.Point](./Point.md)**
      ↳ **OtherIntersection**

## JessieCode 语法

```js
// 创建圆与直线的另一交点
p1 = intersection(c1, l1, 0);  // 第一个交点
p2 = otherintersection(c1, l1, p1);  // 另一个交点

// 创建两圆的另一交点
c1 = circle([0, 0], 3);
c2 = circle([2, 2], 3);
p1 = intersection(c1, c2, 0);
p2 = otherintersection(c1, c2, p1);

// 创建曲线与直线的另一交点
curve = implicitcurve('-(y**2) + x**3 - 2 * x + 1');
A = glider(-1.5, 1, curve);
B = glider(0.5, 0.5, curve);
line = line(A, B);
C = otherintersection(curve, line, [A, B]) << precision: 0.01 >>;

// 创建两曲线的另一交点
c1 = functiongraph('x**2 - 3');
c2 = functiongraph('(x) => -(x**2) + 2 * A.X() * x + A.Y() - A.X()**2');
p1 = intersection(c1, c2);
p2 = otherintersection(c1, c2, [p1]);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| el1 | Line/Circle/Curve | 第一个几何元素（直线、圆或曲线） |
| el2 | Line/Circle/Curve | 第二个几何元素（直线、圆或曲线） |
| p | Point/Array | 已知交点或点数组，新交点将不同于这些点 |

### 父元素组合说明

| 组合 | 描述 |
|------|------|
| `{Line\|Circle}` **el1** + `{Line\|Circle}` **el2** + `{Point\|Array}` **p** | 两个被求交的元素，以及一个或多个已知交点（新交点将不同于这些点） |

## 属性

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `size` | Number | 3 | 点的大小 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 点的名称 |
| `visible` | Boolean | true | 是否可见 |
| `precision` | Number | 0.001 | 数值计算精度（用于曲线交点） |

## 方法

OtherIntersection 继承自 Point，因此具有 Point 的所有方法：

| 方法 | 参数 | 描述 |
|------|------|------|
| `X()` | 无 | 获取 x 坐标 |
| `Y()` | 无 | 获取 y 坐标 |
| `move(dx, dy)` | dx, dy: Number | 移动点 |
| `glide(line)` | line: Line | 使点在直线上滑动 |
| `free()` | 无 | 释放点 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `X(P)` | 获取点 P 的 x 坐标 | `X(p2)` |
| `Y(P)` | 获取点 P 的 y 坐标 | `Y(p2)` |

## 示例

### 1. 圆与直线的交点

```js
// 创建圆心和半径
p1 = point(2.0, 2.0);
c1 = circle(p1, 2.0);

// 创建直线
p2 = point(2.0, 2.0);
p3 = point(2.0, 2.0);
l1 = line(p2, p3);

// 创建第一个交点
ip1 = intersection(c1, l1, 0);

// 创建另一个交点
ip2 = otherintersection(c1, l1, ip1);
```

### 2. 两圆的交点

```js
// 创建两个圆
c1 = circle([0, 0], 3);
c2 = circle([2, 2], 3);

// 创建第一个交点
p1 = intersection(c1, c2, 0);

// 创建另一个交点
p2 = otherintersection(c1, c2, p1);
```

### 3. 曲线与直线的交点（椭圆上的点加法）

```js
// 创建隐式曲线（椭圆）
curve = implicitcurve('-(y**2) + x**3 - 2 * x + 1') << strokeWidth: 2 >>;

// 创建曲线上的滑点
A = glider(-1.5, 1, curve);
B = glider(0.5, 0.5, curve);

// 创建通过两点的直线
line = line(A, B) << color: 'black', strokeWidth: 1 >>;

// 创建第三个交点（另一个交点）
C = otherintersection(curve, line, [A, B]) << precision: 0.01 >>;

// 创建对称点（椭圆上的点加法：A + B = -C）
D = point(() => C.X(), () => -C.Y()) << name: '-C = A + B' >>;
```

### 4. 两函数图像的交点

```js
// 创建两个函数图像
c1 = functiongraph('x**2 - 3') << strokeWidth: 2 >>;
A = point(0, 2);
c2 = functiongraph('(x) => -(x**2) + 2 * A.X() * x + A.Y() - A.X()**2') << strokeWidth: 2 >>;

// 创建第一个交点
p1 = intersection(c1, c2);

// 创建另一个交点
p2 = otherintersection(c1, c2, [p1]);
```

### 5. 动态演示

```js
// 创建可移动的点
center = point(0, 0);
radius = 3;
c1 = circle(center, radius);

// 创建一条可移动的直线
p1 = point(1, 1);
p2 = point(4, 3);
l1 = line(p1, p2);

// 创建两个交点
ip1 = intersection(c1, l1, 0);
ip2 = otherintersection(c1, l1, ip1) <<
    strokeColor: 'red',
    size: 5,
    withLabel: true,
    name: 'P2'
>>;
```

## 注意事项

1. **需要已知交点**：使用 otherintersection 时，必须提供一个或多个已知交点，系统会返回不同于这些点的另一个交点
2. **精度设置**：对于曲线交点，可以通过 `precision` 属性设置数值计算精度，默认值为 0.001
3. **父元素类型**：支持直线 (Line)、圆 (Circle) 和曲线 (Curve) 之间的交点计算
4. **多解情况**：当两个元素有多个交点时（如两圆相交最多有 2 个交点），使用此元素可以获取除已知点外的其他交点
5. **性能考虑**：曲线交点的计算可能比较耗时，尤其是在精度要求较高时

## 相关元素

- [Intersection](./Intersection.md) - 交点
- [Point](./Point.md) - 点
- [Line](./Line.md) - 直线
- [Circle](./Circle.md) - 圆
- [Curve](./Curve.md) - 曲线
- [Implicitcurve](./Implicitcurve.md) - 隐式曲线
- [Functiongraph](./Functiongraph.md) - 函数图像
