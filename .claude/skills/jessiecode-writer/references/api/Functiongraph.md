# Functiongraph 函数图像

<!-- USAGE_FREQUENCY: core -->

## 描述

函数图像用于可视化映射 x → f(x)。图像在区间 [a, b] 上绘制，是 [Curve](./Curve.md) 元素的一种特例。

## JessieCode 语法

```js
// 基本语法 - 创建函数图像
graph = functiongraph(f, a, b);

// 完整定义域（默认 -10 到 10）
graph = functiongraph(f);

// 带属性创建
graph = functiongraph(f, -5, 5) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| f | Function | 函数表达式 |
| a | Number/Function (可选) | 左区间边界，默认 -10 |
| b | Number/Function (可选) | 右区间边界，默认 10 |

## 属性

函数图像继承自 Curve，因此拥有 Curve 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式 |
| `visible` | Boolean | true | 是否可见 |
| `doAdvancedPlot` | Boolean | true | 使用递归细分算法 |
| `firstArrow` | Boolean/Object | false | 起点箭头 |
| `lastArrow` | Boolean/Object | false | 终点箭头 |

## 示例

### 1. 基本函数图像

```js
// 二次函数 f(x) = x²
f1 = functiongraph(function(x) { return x * x; });

// 指定区间
f2 = functiongraph(function(x) { return x * x; }, -3, 3);
```

### 2. 常见函数

```js
// 正弦函数
sinGraph = functiongraph(sin, -2*PI, 2*PI) << strokeColor: 'red' >>;

// 余弦函数
cosGraph = functiongraph(cos, -2*PI, 2*PI) << strokeColor: 'blue' >>;

// 正切函数（注意不连续点）
tanGraph = functiongraph(tan, -PI/2 + 0.1, PI/2 - 0.1) << strokeColor: 'green' >>;

// 指数函数
expGraph = functiongraph(exp, -3, 3) << strokeColor: 'purple' >>;

// 对数函数（x > 0）
logGraph = functiongraph(log, 0.1, 5) << strokeColor: 'orange' >>;
```

### 3. 多项式函数

```js
// 三次函数 f(x) = x³ - 2x + 1
cubic = functiongraph(
    function(x) { return x * x * x - 2 * x + 1; },
    -2, 2
) << strokeWidth: 2 >>;

// 五次函数
quintic = functiongraph(
    function(x) { return 0.1 * x * x * x * x * x - x * x * x + x; },
    -3, 5
);
```

### 4. 动态区间

```js
// 滑块控制右边界
sliderB = slider([0, 4], [4, 4], [-2, 2, 5]);

// 区间可变的函数
graph = functiongraph(
    function(x) { return 0.5 * x * x - 2 * x; },
    -2,
    function() { return V(sliderB); }
);
```

### 5. 多个函数图像比较

```js
// 不同系数的二次函数
f1 = functiongraph(function(x) { return x * x; }, -3, 3) << strokeColor: 'red' >>;
f2 = functiongraph(function(x) { return 2 * x * x; }, -3, 3) << strokeColor: 'blue' >>;
f3 = functiongraph(function(x) { return 0.5 * x * x; }, -3, 3) << strokeColor: 'green' >>;
f4 = functiongraph(function(x) { return -x * x; }, -3, 3) << strokeColor: 'gray' >>;
```

### 6. 函数变换

```js
// 原函数
f = function(x) { return x * x; };
original = functiongraph(f, -3, 3) << strokeColor: 'black', strokeWidth: 2 >>;

// 滑块控制变换
h = slider([1, 4], [4, 4], [-3, 0, 3]) << name: 'h' >>;  // 水平平移
k = slider([-3, 2], [3, 2], [-3, 0, 3]) << name: 'k' >>;  // 垂直平移
a = slider([0.5, 4], [4, 4], [0.5, 1, 3]) << name: 'a' >>;  // 伸缩

// 变换后的函数：y = a*f(x-h) + k
transformed = functiongraph(
    function(x) {
        return V(a) * f(x - V(h)) + V(k);
    },
    -3, 3
) << strokeColor: 'red', dash: 1 >>;
```

### 7. 函数交点

```js
// 两个函数
f = functiongraph(function(x) { return x * x; }, -2, 2) << strokeColor: 'blue' >>;
g = functiongraph(function(x) { return x + 2; }, -2, 2) << strokeColor: 'red' >>;

// 交点需要数值方法求解
// 或使用 intersection 元素（如果支持曲线交点）
```

### 8. 导数函数

```js
// 原函数
f = function(x) { return x * x * x - 3 * x; };
original = functiongraph(f, -2, 2) << strokeColor: 'blue', strokeWidth: 2 >>;

// 导数（数值近似）
derivative = functiongraph(
    function(x) {
        h = 0.001;
        return (f(x + h) - f(x - h)) / (2 * h);
    },
    -2, 2
) << strokeColor: 'red', dash: 1 >>;
```

### 9. 定积分可视化

```js
// 函数
f = functiongraph(function(x) { return -0.1 * x * x + 2; }, -3, 3) <<
    strokeColor: 'blue', strokeWidth: 2 >>;

// 积分上下限
aSlider = slider([-3, -2.5], [-2.5, -2.5], [-3, -2, 3]);
bSlider = slider([2.5, 3], [2.5, 2.5], [-3, 2, 3]);

// 黎曼和近似
// 需要使用 curve 或 polygon 来绘制面积
```

### 10. 参数化函数族

```js
// 滑块控制参数
n = slider([1, 4], [4, 4], [1, 1, 10]);

// 函数族 f(x) = x^n
powerFamily = functiongraph(
    function(x) {
        return pow(x, V(n));
    },
    -2, 2
) << strokeColor: 'blue' >>;

// 三角函数族
omega = slider([1, 4], [4, 4], [0.5, 1, 5]);
waveFamily = functiongraph(
    function(x) {
        return sin(V(omega) * x);
    },
    -2*PI, 2*PI
);
```

### 11. 分段函数

```js
// 分段函数示例
piecewise = functiongraph(
    function(x) {
        if (x < 0) {
            return -x;
        } else if (x < 2) {
            return x * x;
        } else {
            return 2 * x - 2;
        }
    },
    -3, 4
) << strokeWidth: 2 >>;
```

### 12. 隐函数（转换为显函数）

```js
// 圆 x² + y² = 4 需要转换为两个函数
// y = √(4-x²) 和 y = -√(4-x²)

upperCircle = functiongraph(
    function(x) { return sqrt(4 - x * x); },
    -2, 2
) << strokeColor: 'blue' >>;

lowerCircle = functiongraph(
    function(x) { return -sqrt(4 - x * x); },
    -2, 2
) << strokeColor: 'blue' >>;
```

## 注意事项

1. **不连续点**：对于有间断点的函数（如 tan），需要小心指定定义域
2. **动态边界**：区间边界可以是函数，用于创建动画效果
3. **性能**：复杂函数可能需要调整绘图精度属性
4. **隐函数**：圆等隐函数需要转换为显函数形式
5. **曲线类型**：函数图像本质上是一种特殊的参数曲线

## 相关元素

- [Curve](./Curve.md) - 曲线（父类）
- [Slider](./Slider.md) - 滑块（控制参数）
- [Transformation](./Transformation.md) - 变换
