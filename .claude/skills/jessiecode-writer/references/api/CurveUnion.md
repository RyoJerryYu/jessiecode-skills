# CurveUnion 曲线并集

<!-- USAGE_FREQUENCY: advanced -->

## 描述

曲线并集是两个闭合路径元素的并集形成的路径。元素可以是曲线（curve）、圆（circle）、多边形（polygon）或不等式（inequality）类型。如果其中一个元素是曲线，它必须是闭合的。生成的元素是曲线（curve）类型。

## JessieCode 语法

```js
// 基本语法 - 创建两个元素的并集
union = curveunion(element1, element2);

// 带属性创建
union = curveunion(ineq, circ) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| element1 | Curve/Polygon/Circle/Inequality | 第一个定义并集的元素 |
| element2 | Curve/Polygon/Circle/Inequality | 第二个定义并集的元素 |

**注意**：
- 如果其中一个元素是曲线，它必须是闭合的
- 支持的元素类型：曲线、多边形、圆、不等式

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `fillColor` | String | '#ffff00' | 填充颜色 |
| `fillOpacity` | Number | 0.8 | 填充透明度 |
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `visible` | Boolean | true | 是否可见 |

## 示例

### 1. 基本曲线并集

```js
// 创建函数图像
f = functiongraph('cos(x)');

// 创建不等式区域
ineq = inequality([f]) <<
    inverse: true,
    fillOpacity: 0.1
>>;

// 创建圆
circ = circle(point(0, 0), 4);

// 创建并集
union = curveunion(ineq, circ) <<
    fillColor: 'yellow',
    fillOpacity: 0.6
>>;
```

### 2. 两个圆的并集

```js
// 两个相交的圆
c1 = circle(point(-2, 0), 2.5);
c2 = circle(point(2, 0), 2.5);

// 创建并集区域
union = curveunion(c1, c2) <<
    fillColor: 'lightblue',
    fillOpacity: 0.5,
    strokeColor: 'blue'
>>;
```

### 3. 多边形与圆的并集

```js
// 创建多边形
p1 = point(0, 0);
p2 = point(4, 0);
p3 = point(4, 3);
p4 = point(0, 3);
poly = polygon(p1, p2, p3, p4);

// 创建圆
circ = circle(point(2, 1.5), 2);

// 创建并集
union = curveunion(poly, circ) <<
    fillColor: 'lightgreen',
    fillOpacity: 0.4
>>;
```

### 4. 动态并集

```js
// 固定圆
c1 = circle(point(-2, 0), 2);

// 可移动的圆
center = point(2, 0);
c2 = circle(center, 2);

// 动态并集
union = curveunion(c1, c2) <<
    fillColor: 'yellow',
    fillOpacity: 0.5
>>;

// 移动 center 点可以改变并集形状
```

### 5. 多个不等式区域的并集

```js
// 创建两个函数
f1 = functiongraph('sin(x)');
f2 = functiongraph('cos(x)');

// 创建不等式区域
ineq1 = inequality([f1]) <<
    inverse: true,
    fillOpacity: 0.3,
    fillColor: 'red'
>>;

ineq2 = inequality([f2]) <<
    inverse: false,
    fillOpacity: 0.3,
    fillColor: 'blue'
>>;

// 创建并集
union = curveunion(ineq1, ineq2) <<
    fillColor: 'purple',
    fillOpacity: 0.4
>>;
```

### 6. 曲线与多边形的并集

```js
// 创建闭合曲线（参数化圆）
fx1 = function(t) { return 2 * cos(t); };
fy1 = function(t) { return 2 * sin(t); };
curve1 = curve(fx1, fy1, 0, 2*PI);

// 创建多边形
p1 = point(3, 0);
p2 = point(5, 0);
p3 = point(4, 2);
poly = polygon(p1, p2, p3);

// 创建并集
union = curveunion(curve1, poly) <<
    fillColor: 'orange',
    fillOpacity: 0.5
>>;
```

### 7. 可视化集合运算

```js
// 两个相交的圆
c1 = circle(point(-1.5, 0), 2);
c2 = circle(point(1.5, 0), 2);

// 并集
union = curveunion(c1, c2) <<
    fillColor: 'lightyellow',
    fillOpacity: 0.6,
    strokeColor: 'black',
    strokeWidth: 2
>>;

// 显示面积信息
areaText = text(-3, 3, function() {
    return "Union area displayed";
});
```

## 注意事项

1. **闭合曲线**：如果其中一个元素是曲线，它必须是闭合的才能进行并集运算
2. **填充效果**：并集区域可以设置填充颜色和透明度
3. **元素类型**：支持的元素类型包括曲线、圆、多边形和不等式
4. **结果类型**：生成的元素是曲线类型
5. **应用场景**：常用于可视化集合的并集运算、创建复杂形状

## 相关元素

- [Curve](./Curve.md) - 曲线
- [Circle](./Circle.md) - 圆
- [Polygon](./Polygon.md) - 多边形
- [Inequality](./Inequality.md) - 不等式
