# CurveIntersection 曲线交集

## 描述

曲线交集表示两个封闭路径元素的交集。元素可以是曲线、圆、多边形或不等式区域类型。如果其中一个元素是曲线，则该曲线必须是封闭的。结果元素是曲线类型。

交集运算得到两个元素重叠（共同）的部分区域。

## JessieCode 语法

```js
// 基本语法 - 创建两个封闭元素的交集
intersect = curveintersection(element1, element2);

// 带属性创建
intersect = curveintersection(ineq, circ) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| element1 | Curve/Circle/Polygon/Inequality | 第一个元素 |
| element2 | Curve/Circle/Polygon/Inequality | 第二个元素 |

**注意**：
- 两个元素都必须是封闭的路径
- 如果元素是曲线，则该曲线必须是封闭的
- 结果是两个元素重叠（共同）的部分

## 属性

曲线交集继承自 Curve，因此具有所有曲线的属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `fillOpacity` | Number | 0.0 | 填充透明度 |
| `dash` | Number | 0 | 虚线样式 |
| `opacity` | Number | 1.0 | 透明度 |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 元素名称 |

## 示例

### 1. 基本曲线交集

```js
// 创建函数图像
f = functiongraph('cos(x)');

// 创建不等式区域（函数下方区域）
ineq = inequality(f) <<
    inverse: true,
    fillOpacity: 0.1
>>;

// 创建圆
circ = circle(point(0, 0), 4);

// 创建交集：不等式区域与圆的重叠部分
intersect = curveintersection(ineq, circ) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;
```

### 2. 两个圆的交集

```js
// 创建两个相交的圆
c1 = circle(point(-1, 0), 3) <<
    fillColor: 'blue',
    fillOpacity: 0.3
>>;

c2 = circle(point(1, 0), 2) <<
    fillColor: 'red',
    fillOpacity: 0.3
>>;

// 创建交集：两个圆的重叠部分
intersect = curveintersection(c1, c2) <<
    fillColor: 'purple',
    fillOpacity: 0.5
>>;
```

### 3. 多边形与圆的交集

```js
// 创建多边形
A = point(-3, -2);
B = point(3, -2);
C = point(3, 2);
D = point(-3, 2);
poly = polygon(A, B, C, D) <<
    fillColor: 'blue',
    fillOpacity: 0.3
>>;

// 创建圆
circ = circle(point(0, 0), 2) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

// 创建交集：多边形与圆的重叠部分
intersect = curveintersection(poly, circ) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;
```

### 4. 动态曲线交集

```js
// 创建可移动的点
A = point(-3, -2);
B = point(3, -2);
C = point(3, 2);
D = point(-3, 2);

// 创建多边形
poly = polygon(A, B, C, D) <<
    fillColor: 'blue',
    fillOpacity: 0.3
>>;

// 创建可移动的圆
center = point(0, 0);
radiusPoint = point(2, 0);  // 可以拖动改变半径
circ = circle(center, radiusPoint);

// 创建交集
intersect = curveintersection(poly, circ) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;

// 显示交集面积（如果支持）
text(-3, 3, "Intersection area (dynamic)");
```

### 5. 两个不等式区域的交集

```js
// 创建两条直线
l1 = line(0, 1, -1);   // y = x
l2 = line(0, 1, 1);    // y = -x

// 创建两个不等式区域
ineq1 = inequality(l1) <<
    inverse: true,
    fillOpacity: 0.2,
    fillColor: 'blue'
>>;

ineq2 = inequality(l2) <<
    inverse: true,
    fillOpacity: 0.2,
    fillColor: 'red'
>>;

// 创建交集：两个区域的重叠部分
intersect = curveintersection(ineq1, ineq2) <<
    fillColor: 'purple',
    fillOpacity: 0.5
>>;
```

### 6. 封闭曲线与圆的交集

```js
// 创建封闭曲线（椭圆）
ellipse = curve(
    function(t) { return 4 * cos(t); },
    function(t) { return 2 * sin(t); },
    0, 2*PI
) <<
    fillColor: 'blue',
    fillOpacity: 0.3
>>;

// 创建圆
circ = circle(point(0, 0), 1.5) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

// 创建交集：椭圆与圆的重叠部分
intersect = curveintersection(ellipse, circ) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;
```

### 7. 曲线交集的应用：公共区域

```js
// 创建三个圆
c1 = circle(point(-1, 0), 2.5) <<
    fillColor: 'red',
    fillOpacity: 0.2
>>;

c2 = circle(point(1, 0), 2.5) <<
    fillColor: 'green',
    fillOpacity: 0.2
>>;

c3 = circle(point(0, 1.5), 2.5) <<
    fillColor: 'blue',
    fillOpacity: 0.2
>>;

// 创建前两个圆的交集
intersect12 = curveintersection(c1, c2) <<
    fillColor: 'yellow',
    fillOpacity: 0.4
>>;

// 创建三个圆的公共交集（可能需要嵌套）
// intersect123 = curveintersection(intersect12, c3)
```

### 8. 曲线交集与变换

```js
// 创建原始元素
poly = polygon(point(-2, -2), point(2, -2), point(0, 2)) <<
    fillColor: 'blue',
    fillOpacity: 0.3
>>;

circ = circle(point(0, 0), 1.5) <<
    strokeColor: 'red'
>>;

// 创建交集
intersect1 = curveintersection(poly, circ) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;

// 创建平移变换
translate = transform(4, 0) << type: 'translate' >>;

// 变换后的元素
poly2 = curve(poly, translate) <<
    fillColor: 'blue',
    fillOpacity: 0.3
>>;

// 变换后的交集
intersect2 = curveintersection(poly2, circ) <<
    fillColor: 'green',
    fillOpacity: 0.6
>>;
```

### 9. 曲线交集与函数区域

```js
// 创建两个函数
f1 = functiongraph('sin(x)', -PI, PI);
f2 = functiongraph('cos(x)', -PI, PI);

// 创建两个不等式区域
ineq1 = inequality(f1) <<
    inverse: true,
    fillOpacity: 0.2,
    fillColor: 'blue'
>>;

ineq2 = inequality(f2) <<
    inverse: true,
    fillOpacity: 0.2,
    fillColor: 'red'
>>;

// 创建交集：两个函数下方区域的重叠部分
intersect = curveintersection(ineq1, ineq2) <<
    fillColor: 'purple',
    fillOpacity: 0.5
>>;
```

### 10. 曲线交集与差集的组合

```js
// 创建两个圆
c1 = circle(point(-1, 0), 3) <<
    fillColor: 'blue',
    fillOpacity: 0.2
>>;

c2 = circle(point(1, 0), 3) <<
    fillColor: 'red',
    fillOpacity: 0.2
>>;

// 创建交集（重叠部分）
intersect = curveintersection(c1, c2) <<
    fillColor: 'purple',
    fillOpacity: 0.5
>>;

// 创建差集（c1 减去 c2）
diff = curvedifference(c1, c2) <<
    fillColor: 'green',
    fillOpacity: 0.4
>>;

// 显示不同区域
```

### 11. 维恩图（Venn Diagram）

```js
// 创建两个相交的圆（维恩图）
c1 = circle(point(-1.5, 0), 2.5) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

c2 = circle(point(1.5, 0), 2.5) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

// 仅 A 集合（A 减去 B）
onlyA = curvedifference(c1, c2) <<
    fillColor: 'lightblue',
    fillOpacity: 0.5
>>;

// 仅 B 集合（B 减去 A）
onlyB = curvedifference(c2, c1) <<
    fillColor: 'lightcoral',
    fillOpacity: 0.5
>>;

// A 和 B 的交集
intersect = curveintersection(c1, c2) <<
    fillColor: 'purple',
    fillOpacity: 0.5
>>;
```

### 12. 曲线交集的面积计算

```js
// 创建两个圆
c1 = circle(point(0, 0), 3);
c2 = circle(point(2, 0), 3);

// 创建交集
intersect = curveintersection(c1, c2) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;

// 显示交集信息
text(-4, 4, "Intersection of two circles");
text(-4, 3.5, "Radius: 3");
text(-4, 3, "Distance between centers: 2");

// 注意：JessieCode 中可能需要手动计算交集面积
```

## 注意事项

1. **封闭路径**：参与交集运算的元素必须是封闭的路径
2. **曲线封闭性**：如果元素是曲线，则该曲线必须是封闭的（起点和终点重合）
3. **运算交换律**：交集运算满足交换律，`curveintersection(A, B)` 与 `curveintersection(B, A)` 结果相同
4. **填充效果**：交集结果通常需要设置填充颜色和透明度以清晰显示
5. **依赖关系**：交集元素依赖于原始元素，当原始元素变化时交集会自动更新
6. **性能考虑**：复杂的交集运算可能影响渲染性能
7. **无交集情况**：如果两个元素没有重叠部分，交集可能为空或不可见

## 相关元素

- [CurveDifference](./CurveDifference.md) - 曲线差集
- [Curve](./Curve.md) - 曲线
- [Circle](./Circle.md) - 圆
- [Polygon](./Polygon.md) - 多边形
- [Inequality](./Inequality.md) - 不等式区域
- [Transformation](./Transformation.md) - 变换
