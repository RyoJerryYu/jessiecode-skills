# Curve 曲线

## 描述

曲线可以通过参数映射或离散数据集定义。一般来说，曲线是从 R 到 R² 的映射，t 映射到 (x(t), y(t))。图像在区间 [a, b] 上绘制。

## JessieCode 语法

```js
// 参数曲线
curve = curve(xFunc, yFunc, tMin, tMax);

// 数据点曲线
curve = curve(xArray, yArray);

// 带属性创建
curve = curve(fx, fy, 0, 2*PI) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

## 参数

### 参数曲线

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Function/Number/Array | x 坐标函数或数组 |
| y | Function/Number/Array | y 坐标函数或数组 |
| tMin | Number (可选) | 参数起始值，默认 -10 |
| tMax | Number (可选) | 参数结束值，默认 10 |

### 数据曲线

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Array | x 坐标数组 |
| y | Array | y 坐标数组 |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式 |
| `visible` | Boolean | true | 是否可见 |
| `curveType` | String | null | 曲线类型 |
| `doAdvancedPlot` | Boolean | true | 使用递归细分算法 |
| `firstArrow` | Boolean/Object | false | 起点箭头 |
| `lastArrow` | Boolean/Object | false | 终点箭头 |
| `handDrawing` | Boolean | false | 使用贝塞尔曲线连接 |

### 曲线类型 (curveType)

| 值 | 描述 |
|----|------|
| `'parameter'` | 参数曲线 |
| `'functiongraph'` | 函数图像 |
| `'polar'` | 极坐标曲线 |
| `'plot'` | 数据图 |
| `'implicit'` | 隐式曲线 |

## 示例

### 1. 基本参数曲线

```js
// 圆（参数方程）
circle = curve(
    function(t) { return cos(t); },
    function(t) { return sin(t); },
    0, 2*PI
);

// 简化写法
circle = curve(cos, sin, 0, 2*PI);
```

### 2. 摆线（旋轮线）

```js
// 摆线参数方程
cycloid = curve(
    function(t) { return t - sin(t); },
    function(t) { return 1 - cos(t); },
    0, 4*PI
) << strokeWidth: 2 >>;
```

### 3. 数据点曲线

```js
// 数据点
xData = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
yData = [9.2, 1.3, 7.2, -1.2, 4.0, 5.3, 0.2, 6.5, 1.1, 0.0];

// 连接数据点
graph = curve(xData, yData) << dash: 2 >>;
```

### 4. 极坐标曲线

```js
// 心形线 r = a(1 + cos(θ))
a = 1;
cardioid = curve(
    function(phi) { return a * (1 + cos(phi)) * cos(phi); },
    function(phi) { return a * (1 + cos(phi)) * sin(phi); },
    0, 2*PI
) << curveType: 'polar' >>;

// 或使用 slider 控制
sliderA = slider([1, 4], [4, 4], [0.5, 1, 2]);
cardioid2 = curve(
    function(phi) { return V(sliderA) * (1 - cos(phi)) * cos(phi); },
    function(phi) { return V(sliderA) * (1 - cos(phi)) * sin(phi); },
    0, 2*PI
);
```

### 5. 螺旋线

```js
// 阿基米德螺旋
spiral = curve(
    function(t) { return t * cos(t); },
    function(t) { return t * sin(t); },
    0, 6*PI
) << strokeColor: 'blue' >>;

// 对数螺旋
logSpiral = curve(
    function(t) { return exp(0.1 * t) * cos(t); },
    function(t) { return exp(0.1 * t) * sin(t); },
    0, 8*PI
);
```

### 6. 利萨茹曲线

```js
// 利萨茹曲线（频率比 3:2）
lissajous = curve(
    function(t) { return cos(3 * t); },
    function(t) { return sin(2 * t); },
    0, 2*PI
) << strokeColor: 'red', strokeWidth: 2 >>;

// 动态利萨茹曲线
a = slider([1, 4], [4, 4], [1, 3, 10]);
b = slider([1, 3.5], [3.5, 3.5], [1, 2, 10]);
lissajous2 = curve(
    function(t) { return sin(V(a) * t); },
    function(t) { return sin(V(b) * t); },
    0, 2*PI
);
```

### 7. 贝塞尔曲线

```js
// 控制点
P0 = point(-2, -1);
P1 = point(1, 2.5);
P2 = point(-1, -2.5);
P3 = point(2, -2);

// 三次贝塞尔曲线
bezierCurve = curve(
    JXG.Math.Numerics.bezier([P0, P1, P2, P3]),
    0, 1
) << strokeColor: 'red', strokeWidth: 3 >>;
```

### 8. 曲线变换

```js
// 原曲线
cu1 = curve(
    [-1, -1, -0.5, -1, -1, -0.5],
    [-3, -2, -2, -2, -2.5, -2.5]
);

// 反射直线
li = line(1, 1, 1);

// 反射变换
reflect = transform(li) << type: 'reflect' >>;

// 反射后的曲线
cu2 = curve(cu1, reflect) << strokeColor: 'red' >>;
```

### 9. 带箭头的曲线

```js
// 有向曲线
directedCurve = curve(
    function(t) { return t; },
    function(t) { return t * t; },
    -2, 2
) <<
    lastArrow: << type: 7, size: 10 >>,
    strokeWidth: 2
>>;

// 双向箭头
biDirected = curve(
    function(t) { return sin(t); },
    function(t) { return cos(t); },
    0, PI
) <<
    firstArrow: << type: 7 >>,
    lastArrow: << type: 7 >>
>>;
```

### 10. 参数化星形线

```js
// 星形线 x^(2/3) + y^(2/3) = a^(2/3)
a = 2;
astroid = curve(
    function(t) { return a * pow(cos(t), 3); },
    function(t) { return a * pow(sin(t), 3); },
    0, 2*PI
) << strokeColor: 'purple', strokeWidth: 2 >>;
```

### 11. 心脏线

```js
// 心脏线（不同形式）
// 形式 1: r = a(1 - cos(θ))
a = 1.5;
cardioid1 = curve(
    function(t) { return a * (1 - cos(t)) * cos(t); },
    function(t) { return a * (1 - cos(t)) * sin(t); },
    0, 2*PI
);

// 形式 2：使用参数方程的另一种形式
cardioid2 = curve(
    function(t) { return a * (2 * cos(t) - cos(2*t)); },
    function(t) { return a * (2 * sin(t) - sin(2*t)); },
    0, 2*PI
);
```

### 12. 曲线动画

```js
// 动态曲线
tSlider = slider([1, 4], [4, 4], [0, 0, 2*PI]);

// 随滑块增长的螺旋
growingSpiral = curve(
    function(u) { return u * cos(u); },
    function(u) { return u * sin(u); },
    0,
    function() { return V(tSlider); }
);
```

## 注意事项

1. **参数范围**：默认 t 范围是 [-10, 10]，可以通过参数指定
2. **数组曲线**：使用数组时，曲线会依次连接各点
3. **平滑度**：`doAdvancedPlot: true` 可以自动检测不连续点
4. **性能**：复杂曲线可能需要调整 `numberPointsLow/High` 属性
5. **曲线类型**：使用 `curveType: 'polar'` 可以创建极坐标曲线

## 相关元素

- [Functiongraph](./Functiongraph.md) - 函数图像
- [Arc](./Arc.md) - 圆弧
- [Glider](./Glider.md) - 滑点（可在曲线上滑动）
