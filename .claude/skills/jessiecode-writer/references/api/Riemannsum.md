# Riemannsum 黎曼和

<!-- USAGE_FREQUENCY: common -->

## 描述

黎曼和用于可视化积分的近似值，通过有限和来逼近定积分。它被实现为一种特殊的曲线。返回的元素具有 `Value()` 方法，用于计算所有矩形条的面积之和。

在类型设置为 "simpson"（辛普森）和 "trapezoidal"（梯形）时，近似函数值的水平线会被抛物线或割线替代。对于 "simpson" 类型，抛物线在视觉上通过固定步宽的多边形链来近似。

## JessieCode 语法

```js
// 基本语法 - 创建黎曼和
r = riemannsum(f, n, type, a, b);

// 使用函数创建
f = function(x) { return 0.5*x*x - 2*x; };
r = riemannsum(f, 10, 'left', -2, 5);

// 使用滑块控制矩形数量
s = slider([0, 4], [3, 4], [0, 4, 10]) << snapWidth: 1 >>;
r = riemannsum(f, function() { return V(s); }, 'upper', -2, 5);

// 带属性创建
r = riemannsum(f, 20, 'middle', -2, 5) <<
    strokeColor: 'blue',
    fillColor: 'lightblue',
    fillOpacity: 0.4
>>;

// 两个函数之间的黎曼和
g = function(x) { return -x*(x-4); };
f = function(x) { return 0.5*x*x - 2*x; };
r = riemannsum([g, f], 15, 'lower', 0, 4);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| f | Function/Array | 函数项 f(x) 定义函数图像，或由两个函数组成的数组，填充两函数之间的区域 |
| n | Number/Function | 矩形条的数量，可以是固定数字或返回数字的函数 |
| type | String/Function (可选) | 黎曼和类型，可选值：'left'、'right'、'middle'、'lower'、'upper'、'random'、'simpson'、'trapezoidal'，默认 'left' |
| a | Number/Function (可选) | 积分区间左边界，默认 -10 |
| b | Number/Function (可选) | 积分区间右边界，默认 10 |

### 黎曼和类型说明

| 类型 | 描述 |
|------|------|
| `'left'` | 左黎曼和：使用每个子区间左端点的函数值 |
| `'right'` | 右黎曼和：使用每个子区间右端点的函数值 |
| `'middle'` | 中点黎曼和：使用每个子区间中点的函数值 |
| `'lower'` | 下和：使用每个子区间的最小函数值 |
| `'upper'` | 上和：使用每个子区间的最大函数值 |
| `'random'` | 随机黎曼和：使用每个子区间的随机点函数值 |
| `'simpson'` | 辛普森法则（1/3 法则）：使用抛物线近似 |
| `'trapezoidal'` | 梯形法则：使用割线近似 |

## 属性

黎曼和继承自 Curve，因此可以使用 Curve 的所有属性。

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 1 | 线宽 |
| `fillColor` | String | '#ffff00' | 填充颜色 |
| `fillOpacity` | Number | 0.5 | 填充透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `Value()` | 无 | 获取黎曼和的值，即所有矩形条面积之和（带符号） |

## 示例

### 1. 基本黎曼和

```js
// 定义函数
f = function(x) { return 0.5*x*x - 2*x; };

// 左黎曼和
leftSum = riemannsum(f, 10, 'left', -2, 5);

// 右黎曼和
rightSum = riemannsum(f, 10, 'right', -2, 5);

// 中点黎曼和
middleSum = riemannsum(f, 10, 'middle', -2, 5);
```

### 2. 使用滑块动态调整

```js
// 创建滑块控制矩形数量
s = slider([0, 4], [3, 4], [0, 4, 10]) << snapWidth: 1 >>;

// 定义函数
f = function(x) { return 0.5*x*x - 2*x; };

// 创建黎曼和，矩形数量随滑块变化
r = riemannsum(f, function() { return V(s); }, 'upper', -2, 5) <<
    fillOpacity: 0.4
>>;

// 创建函数图像
g = functiongraph(f, -2, 5);

// 显示黎曼和的值
t = text(-2, -2, function() {
    return 'Sum = ' + f(r.Value(), 4);
});
```

### 3. 不同黎曼和类型比较

```js
// 定义函数
f = function(x) { return 0.25*x*x; };

// 上和
upper = riemannsum(f, 8, 'upper', 0, 4) <<
    fillColor: 'red',
    fillOpacity: 0.3
>>;

// 下和
lower = riemannsum(f, 8, 'lower', 0, 4) <<
    fillColor: 'blue',
    fillOpacity: 0.3
>>;

// 梯形法则
trap = riemannsum(f, 8, 'trapezoidal', 0, 4) <<
    strokeColor: 'green',
    strokeWidth: 2
>>;

// 辛普森法则
simp = riemannsum(f, 8, 'simpson', 0, 4) <<
    strokeColor: 'purple',
    strokeWidth: 2
>>;
```

### 4. 两个函数之间的黎曼和

```js
// 创建滑块
s = slider([0, 4], [3, 4], [0, 4, 10]) << snapWidth: 1 >>;

// 定义两个函数
g = function(x) { return 0.5*x*x - 2*x; };
f = function(x) { return -x*(x-4); };

// 两个函数之间的黎曼和
r = riemannsum([g, f], function() { return V(s); }, 'lower', 0, 4) <<
    fillOpacity: 0.4
>>;

// 创建两个函数图像
fg = functiongraph(g, -2, 5);
ff = functiongraph(f, -2, 5);

// 显示黎曼和的值
t = text(-2, -2, function() {
    return 'Sum = ' + f(r.Value(), 4);
});
```

### 5. 随机黎曼和

```js
// 定义函数
f = function(x) { return sin(x) + 2; };

// 随机黎曼和
randomSum = riemannsum(f, 20, 'random', 0, 2*PI) <<
    fillColor: 'orange',
    fillOpacity: 0.5
>>;
```

### 6. 辛普森法则可视化

```js
// 定义函数
f = function(x) { return exp(-x*x/2); };

// 辛普森法则（抛物线近似）
simpson = riemannsum(f, 10, 'simpson', -3, 3) <<
    strokeColor: 'red',
    strokeWidth: 2,
    fillColor: 'lightblue',
    fillOpacity: 0.4
>>;

// 函数图像
curve = functiongraph(f, -3, 3) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

### 7. 黎曼和动画

```js
// 创建滑块控制矩形数量
n = slider([1, 4], [4, 4], [1, 50, 1]) <<
    name: 'n',
    withLabel: true
>>;

// 定义函数
f = function(x) { return 0.1*x*x*x - 0.5*x*x + 2; };

// 动态黎曼和
r = riemannsum(f, function() { return V(n); }, 'middle', -2, 6) <<
    fillOpacity: 0.5
>>;

// 函数图像
g = functiongraph(f, -2, 6);

// 显示当前值
t = text(-2, 4, function() {
    return 'n = ' + f(V(n), 0) + ', Sum = ' + f(r.Value(), 4);
});
```

### 8. 积分近似比较

```js
// 定义函数
f = function(x) { return cos(x); };

// 各种近似方法
left = riemannsum(f, 12, 'left', 0, PI) << fillColor: 'red', fillOpacity: 0.3 >>;
right = riemannsum(f, 12, 'right', 0, PI) << fillColor: 'blue', fillOpacity: 0.3 >>;
middle = riemannsum(f, 12, 'middle', 0, PI) << fillColor: 'green', fillOpacity: 0.3 >>;
trap = riemannsum(f, 12, 'trapezoidal', 0, PI) << strokeColor: 'purple', strokeWidth: 2 >>;
simp = riemannsum(f, 12, 'simpson', 0, PI) << strokeColor: 'orange', strokeWidth: 2 >>;

// 精确值显示（sin(PI) - sin(0) = 0）
exact = text(1, -0.5, 'Exact: 0');
```

## 注意事项

1. **矩形数量**：n 值越大，近似越精确，但计算量也越大
2. **类型选择**：辛普森法则和梯形法则通常比左/右黎曼和更精确
3. **符号面积**：`Value()` 返回的是带符号的面积和，x 轴下方为负
4. **两函数之间**：使用数组 `[g, f]` 可以计算两个函数之间的黎曼和
5. **动态更新**：参数可以是函数，实现动态更新的黎曼和
6. **视觉近似**：辛普森法则的抛物线在视觉上通过多边形链近似

## 相关元素

- [Functiongraph](./Functiongraph.md) - 函数图像
- [Curve](./Curve.md) - 曲线
- [Integral](./Integral.md) - 积分
