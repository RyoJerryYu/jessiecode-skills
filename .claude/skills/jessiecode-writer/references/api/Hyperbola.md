# Hyperbola 双曲线

## 描述

双曲线是一种特殊的圆锥曲线，由两个焦点和双曲线上的第三个点定义，或由两个焦点和实轴长度定义。

## JessieCode 语法

```js
// 通过三个点创建双曲线
hyperbola = hyperbola(focus1, focus2, pointOnHyperbola);

// 通过两个焦点和实轴长度创建
hyperbola = hyperbola(focus1, focus2, transverseAxisLength);

// 带属性创建
hyperbola = hyperbola(F1, F2, P) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

## 参数

### 方式一：三个点

| 参数 | 类型 | 描述 |
|------|------|------|
| focus1 | Point/Array | 第一个焦点 |
| focus2 | Point/Array | 第二个焦点 |
| pointOnHyperbola | Point/Array | 双曲线上的点 |

### 方式二：两个焦点加实轴

| 参数 | 类型 | 描述 |
|------|------|------|
| focus1 | Point/Array | 第一个焦点 |
| focus2 | Point/Array | 第二个焦点 |
| transverseAxisLength | Number/Function | 实轴长度 |

## 属性

双曲线继承自 Conic，因此拥有 Conic 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式 |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |

## 示例

### 1. 创建基本双曲线

```js
// 三个点定义双曲线
F1 = point(-1, 4);   // 焦点 1
F2 = point(-1, -4);  // 焦点 2
P = point(1, 1);     // 双曲线上的点

hyperbola1 = hyperbola(F1, F2, P);
```

### 2. 使用实轴长度

```js
// 两个焦点
F1 = point(-3, 0);
F2 = point(3, 0);

// 实轴长度 = 4
hyperbola2 = hyperbola(F1, F2, 4);
```

### 3. 动态双曲线

```js
// 可移动的焦点
F1 = point(-2, 0);
F2 = point(2, 0);

// 可移动的点
P = point(1, 0);

// 动态双曲线
hyperbola = hyperbola(F1, F2, P) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 显示 |PF1 - PF2| = 常数
diffDist = text(0, 3, function() {
    return "|PF1 - PF2| = " + Math.abs(dist(P, F1) - dist(P, F2)).toFixed(2);
});
```

### 4. 双曲线定义演示

```js
// 焦点
F1 = point(-3, 0);
F2 = point(3, 0);

// 双曲线上的动点
P = glider(hyperbola(F1, F2, 2));

// 绘制线段
r1 = segment(P, F1) << strokeColor: 'red' >>;
r2 = segment(P, F2) << strokeColor: 'blue' >>;

// 显示距离差
diffText = text(0, 4, function() {
    d1 = dist(P, F1);
    d2 = dist(P, F2);
    return "|d1 - d2| = " + Math.abs(d1 - d2).toFixed(2);
});
```

### 5. 共焦点双曲线族

```js
// 共同焦点
F1 = point(-2, 0);
F2 = point(2, 0);

// 不同实轴长度的双曲线
h1 = hyperbola(F1, F2, 1) << strokeColor: 'red' >>;
h2 = hyperbola(F1, F2, 2) << strokeColor: 'blue' >>;
h3 = hyperbola(F1, F2, 3) << strokeColor: 'green' >>;
```

### 6. 双曲线与椭圆对比

```js
// 共同焦点
F1 = point(-2, 0);
F2 = point(2, 0);
P = point(3, 0);

// 椭圆（距离和为常数）
ellipse1 = ellipse(F1, F2, P) <<
    strokeColor: 'blue',
    dash: 1
>>;

// 双曲线（距离差为常数）
hyperbola1 = hyperbola(F1, F2, P) <<
    strokeColor: 'red'
>>;
```

### 7. 双曲线的渐近线

```js
// 双曲线
F1 = point(-3, 0);
F2 = point(3, 0);
h = hyperbola(F1, F2, 4);

// 中心
C = midpoint(F1, F2);

// 渐近线需要通过其他方式构造
// 双曲线 y = ±(b/a)x 的形式
// 对于这个双曲线：a = 2, c = 3, b = √(c²-a²) = √5
// 渐近线斜率 = b/a = √5/2
```

### 8. 等轴双曲线

```js
// 等轴双曲线 xy = 1
// 可以通过参数方程创建曲线
rectHyperbola = curve(
    function(t) { return t; },
    function(t) { return 1 / t; },
    -3, -0.1
);

// 另一支
rectHyperbola2 = curve(
    function(t) { return t; },
    function(t) { return 1 / t; },
    0.1, 3
) << strokeColor: 'blue' >>;
```

### 9. 双曲线反射性质

```js
// 双曲线的光学性质：从一个焦点发出的光
// 经双曲线反射后，反射光线的反向延长线经过另一个焦点

F1 = point(-3, 0) <<
    strokeColor: 'red',
    fillColor: 'red',
    size: 5
>>;
F2 = point(3, 0) <<
    strokeColor: 'red',
    fillColor: 'red',
    size: 5
>>;

h = hyperbola(F1, F2, 4);

// 双曲线上的点
P = glider(h);

// 入射光线和反射光线
// 需要通过切线和法线来演示
```

### 10. 双曲线参数变化

```js
// 滑块控制实轴长度
aSlider = slider([1, 4], [4, 4], [0.5, 2, 4]) << name: 'a' >>;

// 固定焦点
F1 = point(-3, 0);
F2 = point(3, 0);

// 动态双曲线
dynamicHyperbola = hyperbola(F1, F2, function() {
    return V(aSlider);
});
```

## 注意事项

1. **几何定义**：双曲线上任意点到两焦点的距离之差的绝对值为常数（等于实轴长度）
2. **两支曲线**：双曲线有两支，分别位于两个焦点的外侧
3. **离心率**：e = c/a > 1（双曲线的离心率大于 1）
4. **渐近线**：双曲线有两条渐近线，曲线无限接近但永不相交

## 相关元素

- [Conic](./Conic.md) - 圆锥曲线（父类）
- [Ellipse](./Ellipse.md) - 椭圆
- [Parabola](./Parabola.md) - 抛物线
- [Curve](./Curve.md) - 曲线
