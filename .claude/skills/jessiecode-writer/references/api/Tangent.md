# Tangent 切线

## 描述

切线是在曲线、圆、圆锥曲线或直线上的某一点处与该元素相切的直线。切线由一个滑点（glider）和它所依附的元素定义。

## JessieCode 语法

```js
// 通过滑点创建切线
tangent = tangent(glider);

// 通过点和曲线创建
tangent = tangent(point, curve);

// 带属性创建
t = tangent(g) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| glider | Glider | 在曲线、圆或直线上的滑点 |
| curve | Curve/Circle/Conic (可选) | 切线所依附的曲线 |

## 属性

切线继承自 Line，因此拥有 Line 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式 |
| `visible` | Boolean | true | 是否可见 |

## 示例

### 1. 函数图像的切线

```js
// 函数图像
f = functiongraph(function(x) { return x * x; }, -2, 2);

// 滑点
g = glider(f);

// 切线
t = tangent(g) << strokeColor: 'red' >>;

// 显示斜率
slopeText = text(1, 3, function() {
    return "Slope: " + (2 * g.X()).toFixed(2);
});
```

### 2. 圆的切线

```js
// 圆
O = point(0, 0);
c = circle(O, 2);

// 圆上的滑点
P = glider(c);

// 切线
t = tangent(P) << strokeColor: 'blue' >>;

// 半径
r = segment(O, P) << strokeColor: 'gray', dash: 1 >>;

// 切线垂直于半径
rightAngle = angle(O, P, point(1, 0)) <<
    radius: 0.5,
    type: 'square'
>>;
```

### 3. 动态切线演示

```js
// 抛物线
p = functiongraph(function(x) { return 0.5 * x * x; }, -3, 3);

// 滑点
g = glider(p);

// 切线
t = tangent(g) << strokeColor: 'red', strokeWidth: 2 >>;

// 显示切线方程
// y = f'(a)(x-a) + f(a)
tangentEq = text(-3, 4, function() {
    a = g.X();
    fa = 0.5 * a * a;
    fp = a;  // 导数
    return "y = " + fp.toFixed(2) + "x + " + (fa - fp * a).toFixed(2);
});
```

### 4. 椭圆的切线

```js
// 椭圆
F1 = point(-2, 0);
F2 = point(2, 0);
e = ellipse(F1, F2, point(3, 0));

// 椭圆上的滑点
P = glider(e);

// 切线
t = tangent(P) << strokeColor: 'blue' >>;

// 焦点到切点的连线
r1 = segment(F1, P) << strokeColor: 'gray' >>;
r2 = segment(F2, P) << strokeColor: 'gray' >>;

// 椭圆的光学性质：切线平分焦点连线的外角
```

### 5. 双曲线的切线

```js
// 双曲线
F1 = point(-3, 0);
F2 = point(3, 0);
h = hyperbola(F1, F2, 4);

// 双曲线上的滑点
P = glider(h);

// 切线
t = tangent(P) << strokeColor: 'red' >>;
```

### 6. 导数的几何意义

```js
// 函数
f = functiongraph(function(x) {
    return x * x * x - 3 * x;
}, -2, 2) << strokeColor: 'blue', strokeWidth: 2 >>;

// 滑点
g = glider(f);

// 切线
tan = tangent(g) << strokeColor: 'red' >>;

// 导数图像（数值近似）
deriv = functiongraph(
    function(x) {
        h = 0.001;
        return ((x+h)*(x+h)*(x+h) - 3*(x+h) - ((x-h)*(x-h)*(x-h) - 3*(x-h))) / (2*h);
    },
    -2, 2
) << strokeColor: 'green', dash: 1 >>;

// 显示导数值
derivText = text(-2, 3, function() {
    return "f'(" + g.X().toFixed(2) + ") = " + (3 * g.X() * g.X() - 3).toFixed(2);
});
```

### 7. 参数曲线的切线

```js
// 参数曲线（圆）
c = curve(cos, sin, 0, 2*PI);

// 滑点
g = glider(c);

// 切线
t = tangent(g) << strokeColor: 'red' >>;

// 或使用参数曲线
spiral = curve(
    function(t) { return t * cos(t); },
    function(t) { return t * sin(t); },
    0, 4*PI
);
```

### 8. 多条切线比较

```js
// 函数
f = functiongraph(function(x) { return sin(x); }, 0, 2*PI);

// 多个滑点
g1 = glider(f) << strokeColor: 'red' >>;
g2 = glider(f) << strokeColor: 'blue' >>;
g3 = glider(f) << strokeColor: 'green' >>;

// 多条切线
t1 = tangent(g1) << strokeColor: 'red' >>;
t2 = tangent(g2) << strokeColor: 'blue' >>;
t3 = tangent(g3) << strokeColor: 'green' >>;
```

### 9. 切线动画

```js
// 函数
f = functiongraph(function(x) { return x * x; }, -2, 2);

// 滑点
g = glider(f);

// 切线
t = tangent(g) << strokeColor: 'red', strokeWidth: 2 >>;

// 动画按钮
animateBtn = button(-3, 4, "Animate", function() {
    g.startAnimation(1, 100, 50, -1);
});

stopBtn = button(1, 4, "Stop", function() {
    g.stopAnimation();
});
```

### 10. 抛物线的光学性质

```js
// 抛物线 y = x²/4
// 焦点 (0, 1)
F = point(0, 1) <<
    strokeColor: 'red',
    fillColor: 'red',
    size: 5,
    name: 'F'
>>;

// 准线 y = -1
directrix = line(point(-3, -1), point(3, -1)) << dash: 1 >>;

// 抛物线
p = parabola(F, directrix);

// 抛物线上的点
P = glider(p);

// 切线
tan = tangent(P) << strokeColor: 'blue' >>;

// 入射光线（平行于轴）
// 反射光线（指向焦点）
// 入射角等于反射角
```

## 注意事项

1. **滑点必需**：切线需要一个滑点来定义切点位置
2. **曲线类型**：切线可以用于函数图像、圆、椭圆、双曲线、抛物线等
3. **垂直关系**：圆的切线垂直于过切点的半径
4. **光学性质**：圆锥曲线的切线有特殊的光学反射性质

## 相关元素

- [Line](./Line.md) - 直线（父类）
- [Glider](./Glider.md) - 滑点
- [Functiongraph](./Functiongraph.md) - 函数图像
- [Circle](./Circle.md) - 圆
- [Ellipse](./Ellipse.md) - 椭圆
- [Hyperbola](./Hyperbola.md) - 双曲线
- [Parabola](./Parabola.md) - 抛物线
