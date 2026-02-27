# CurveDifference 曲线差集

## 描述

曲线差集表示两个封闭路径元素的差集。元素可以是曲线、圆、多边形或不等式区域类型。如果其中一个元素是曲线，则该曲线必须是封闭的。结果元素是曲线类型。

差集运算从第一个元素中"减去"第二个元素，得到第一个元素中不与第二个元素重叠的部分。

## JessieCode 语法

```js
// 基本语法 - 创建两个封闭元素的差集
diff = curvedifference(element1, element2);

// 带属性创建
diff = curvedifference(ineq, circ) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| element1 | Curve/Circle/Polygon/Inequality | 第一个元素（被减去的元素） |
| element2 | Curve/Circle/Polygon/Inequality | 第二个元素（被减去的元素） |

**注意**：
- 两个元素都必须是封闭的路径
- 如果元素是曲线，则该曲线必须是封闭的
- 结果是从 element1 中减去 element2 的部分

## 属性

曲线差集继承自 Curve，因此具有所有曲线的属性：

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

### 1. 基本曲线差集

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

// 创建差集：不等式区域减去圆
diff = curvedifference(ineq, circ) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;
```

### 2. 两个圆的差集

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

// 创建差集：c1 减去 c2
diff = curvedifference(c1, c2) <<
    fillColor: 'green',
    fillOpacity: 0.5
>>;
```

### 3. 多边形与圆的差集

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

// 创建差集：多边形减去圆
diff = curvedifference(poly, circ) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;
```

### 4. 动态曲线差集

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
radiusPoint = point(2, 0);
circ = circle(center, radiusPoint);

// 创建差集
diff = curvedifference(poly, circ) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;

// 显示面积
text(-3, 3, function() {
    return "Area: (dynamic calculation)";
});
```

### 5. 两个不等式区域的差集

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

// 创建差集
diff = curvedifference(ineq1, ineq2) <<
    fillColor: 'green',
    fillOpacity: 0.5
>>;
```

### 6. 封闭曲线与圆的差集

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

// 创建差集：椭圆减去圆
diff = curvedifference(ellipse, circ) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;
```

### 7. 曲线差集的应用：环形区域

```js
// 创建两个同心圆
O = point(0, 0);
c1 = circle(O, 3) <<
    fillColor: 'blue',
    fillOpacity: 0.3
>>;

c2 = circle(O, 1.5) <<
    fillColor: 'white',
    fillOpacity: 1
>>;

// 创建环形区域（大圆减去小圆）
annulus = curvedifference(c1, c2) <<
    fillColor: 'blue',
    fillOpacity: 0.5
>>;
```

### 8. 曲线差集与变换

```js
// 创建原始元素
poly = polygon(point(-2, -2), point(2, -2), point(0, 2)) <<
    fillColor: 'blue',
    fillOpacity: 0.3
>>;

circ = circle(point(0, 0), 1) <<
    strokeColor: 'red'
>>;

// 创建差集
diff1 = curvedifference(poly, circ) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;

// 创建平移变换
translate = transform(5, 0) << type: 'translate' >>;

// 变换后的差集
diff2 = curve(diff1, translate) <<
    fillColor: 'green',
    fillOpacity: 0.6
>>;
```

### 9. 曲线差集与函数区域

```js
// 创建两个函数
f1 = functiongraph('sin(x)', -PI, PI);
f2 = functiongraph('cos(x)', -PI, PI);

// 创建不等式区域
ineq1 = inequality(f1) <<
    inverse: true,
    fillOpacity: 0.2,
    fillColor: 'blue'
>>;

ineq2 = inequality(f2) <<
    fillOpacity: 0.2,
    fillColor: 'red'
>>;

// 创建差集
diff = curvedifference(ineq1, ineq2) <<
    fillColor: 'purple',
    fillOpacity: 0.5
>>;
```

### 10. 多重差集

```js
// 创建大矩形
poly1 = polygon(
    point(-4, -3),
    point(4, -3),
    point(4, 3),
    point(-4, 3)
) << fillColor: 'blue', fillOpacity: 0.3 >>;

// 创建两个小圆
c1 = circle(point(-1.5, 0), 1);
c2 = circle(point(1.5, 0), 1);

// 第一次差集
diff1 = curvedifference(poly1, c1) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;

// 第二次差集（从结果中再减去一个圆）
// 注意：这可能需要嵌套使用
diff2 = curvedifference(diff1, c2) <<
    fillColor: 'green',
    fillOpacity: 0.6
>>;
```

## 注意事项

1. **封闭路径**：参与差集运算的元素必须是封闭的路径
2. **曲线封闭性**：如果元素是曲线，则该曲线必须是封闭的（起点和终点重合）
3. **运算顺序**：差集运算不满足交换律，`curvedifference(A, B)` 与 `curvedifference(B, A)` 结果不同
4. **填充效果**：差集结果通常需要设置填充颜色和透明度以清晰显示
5. **依赖关系**：差集元素依赖于原始元素，当原始元素变化时差集会自动更新
6. **性能考虑**：复杂的差集运算可能影响渲染性能

## 相关元素

- [CurveIntersection](./CurveIntersection.md) - 曲线交集
- [Curve](./Curve.md) - 曲线
- [Circle](./Circle.md) - 圆
- [Polygon](./Polygon.md) - 多边形
- [Inequality](./Inequality.md) - 不等式区域
- [Transformation](./Transformation.md) - 变换
