# Glider 滑点

## 描述

滑点是依附于另一个几何元素（如直线、圆、曲线等）上的点。滑点可以沿着其依附的元素自由移动。

## JessieCode 语法

```js
// 基本语法 - 在圆上创建滑点
G = glider(circle);

// 在直线上创建滑点
G = glider(line);

// 在曲线上创建滑点
G = glider(curve);

// 指定初始坐标
G = glider(x, y, circle);

// 带属性创建
G = glider(c) <<
    strokeColor: 'red',
    size: 5
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Number (可选) | 初始 x 坐标（默认 0） |
| y | Number (可选) | 初始 y 坐标（默认 0） |
| glideObject | Line/Circle/Curve/Point | 滑点依附的元素 |

**注意**：如果提供的坐标不在依附元素上，滑点会被投影到该元素上。

## 属性

滑点继承自 Point，因此拥有 Point 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `size` | Number | 3 | 点的大小 |
| `face` | String | 'circle' | 点的样式 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `visible` | Boolean | true | 是否可见 |
| `fixed` | Boolean | false | 是否固定 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `startAnimation(direction, stepCount, delay, maxRounds)` | 启动动画 |
| `stopAnimation()` | 停止动画 |
| `setPosition(position)` | 设置位置 |
| `X()` | 获取 x 坐标 |
| `Y()` | 获取 y 坐标 |

### startAnimation 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| direction | Number | 方向：+1（正向）或 -1（反向） |
| stepCount | Number | 分成的步数（至少为 1） |
| delay | Number | 每步间隔时间（毫秒），默认 250 |
| maxRounds | Number | 运行圈数，负数或 Infinity 表示无限循环 |

## 示例

### 1. 在圆上创建滑点

```js
// 创建圆
O = point(2, 2);
c = circle(O, 2);

// 在圆上创建滑点
G = glider(c);

// 或指定初始位置
G2 = glider(3, 3, c);  // 会被投影到圆上
```

### 2. 在直线上创建滑点

```js
// 创建直线
A = point(0, 0);
B = point(4, 4);
l = line(A, B);

// 在直线上创建滑点
G = glider(l);

// 或指定初始位置
G2 = glider(1, 0, l);  // 会被投影到直线上
```

### 3. 在曲线上创建滑点

```js
// 创建抛物线
f = functiongraph(function(x) { return x * x; }, -2, 2);

// 在曲线上创建滑点
G = glider(f);

// 滑点 G 可以沿抛物线移动
```

### 4. 滑点动画

```js
// 创建圆和滑点
c = circle(point(0, 0), 2);
G = glider(c);

// 启动动画
// 方向 1（逆时针），6 步，每步 330ms
// G.startAnimation(1, 6, 330);

// 或使用按钮控制
startBtn = button([1, 3, "Start"], function() {
    G.startAnimation(1, 60, 100);
});

stopBtn = button([1, 2, "Stop"], function() {
    G.stopAnimation();
});
```

### 5. 滑块（特殊滑点）

```js
// 滑块是特殊的滑点
s = slider([1, 2], [3, 2], [1, 5, 10]);
// 范围 1-10，初始值 5

// 使用滑块值
text(1, 3, "Value: " + V(s));

// 控制其他元素
c = circle(point(0, 0), function() { return V(s); });
```

### 6. 滑点追踪轨迹

```js
// 创建圆和滑点
c = circle(point(0, 0), 2);
G = glider(c);

// 创建轨迹
// 注意：JessieCode 中可能需要使用 locus 元素
// locus = locus(G, ...);

// 或使用曲线近似
// 通过记录位置创建轨迹曲线
```

### 7. 滑点依附于多边形边

```js
// 三角形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);
pol = polygon(A, B, C);

// 在边上创建滑点
G1 = glider(pol.borders[0]);  // 在 AB 边上
G2 = glider(pol.borders[1]);  // 在 BC 边上
G3 = glider(pol.borders[2]);  // 在 AC 边上
```

### 8. 滑点测量距离

```js
// 圆
c = circle(point(0, 0), 2);

// 滑点
G = glider(c);

// 固定点
A = point(3, 0);

// 显示距离
distText = text(1, 3, function() {
    return "Distance: " + dist(G, A).toFixed(2);
});
```

### 9. 多个滑点组合

```js
// 圆
c = circle(point(0, 0), 2);

// 两个滑点
G1 = glider(c);
G2 = glider(c);

// 连接线段
s = segment(G1, G2);

// 显示弦长
chordText = text(1, 3, function() {
    return "Chord Length: " + L(s).toFixed(2);
});
```

### 10. 滑点与角度

```js
// 圆
O = point(0, 0);
c = circle(O, 2);

// 固定点
A = point(2, 0);

// 滑点
B = glider(c);

// 圆心角
centerAngle = angle(A, O, B) <<
    radius: 0.8,
    fillColor: 'lightblue'
>>;

// 显示角度
angleText = text(1, 3, function() {
    return "Angle: " + centerAngle.Value('degrees').toFixed(1) + "°";
});
```

### 11. 滑点参数化曲线

```js
// 椭圆参数方程
fx = function(t) { return 3 * cos(t); };
fy = function(t) { return 2 * sin(t); };

// 创建椭圆曲线
ellipse = curve(fx, fy, 0, 2*PI);

// 在椭圆上创建滑点
G = glider(ellipse);

// 滑点 G 可以沿椭圆移动
```

### 12. 滑点动画控制

```js
// 创建基础元素
c = circle(point(0, 0), 2);
G = glider(c);

// 动画控制按钮
forwardBtn = button([-3, 3, "Forward >>"], function() {
    G.startAnimation(1, 100, 50, 1);
});

backwardBtn = button([-3, 2.5, "<< Backward"], function() {
    G.startAnimation(-1, 100, 50, 1);
});

stopBtn = button([-3, 2, "Stop"], function() {
    G.stopAnimation();
});
```

## 注意事项

1. **投影**：如果初始坐标不在依附元素上，滑点会被自动投影到该元素
2. **动画**：使用 `startAnimation()` 启动动画，`stopAnimation()` 停止
3. **滑块**：Slider 是 Glider 的特殊形式，专门用于数值选择
4. **自由度**：滑点只能沿依附元素移动，不能离开该元素
5. **曲线长度**：对于闭合曲线（如圆），动画可以无限循环

## 相关元素

- [Point](./Point.md) - 点
- [Slider](./Slider.md) - 滑块
- [Circle](./Circle.md) - 圆
- [Line](./Line.md) - 直线
- [Curve](./Curve.md) - 曲线
