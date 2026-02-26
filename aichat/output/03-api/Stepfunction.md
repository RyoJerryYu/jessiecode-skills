# Stepfunction 阶跃函数

## 描述

阶跃函数是一种分段为常数的函数图像。如果数据点需要在创建后更新，可以通过 `curve.xTerm` 和 `curve.yTerm` 访问。

阶跃函数继承自 [Curve](./Curve.md)，因此拥有曲线的所有属性和方法。

## 继承关系

**[JXG.GeometryElement](./GeometryElement.md)**
   ↳ **[JXG.Curve](./Curve.md)**
         ↳ **Stepfunction**

## JessieCode 语法

```js
// 基本语法 - 创建阶跃函数
step = stepfunction(xArray, yArray);

// 带属性创建
step = stepfunction([0, 1, 2, 3, 4, 5], [1, 3, 0, 2, 2, 1]) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| xArray | Array/Function | 包含 x 坐标的数组或返回数组的函数 |
| yArray | Array/Function | 包含 y 坐标的数组或返回数组的函数 |

**说明**：
- `xArray` 和 `yArray` 必须是长度相同的数组
- 数组元素可以是数字或返回数字的函数
- 阶跃函数会在每个区间 `[x[i], x[i+1])` 上保持常数值 `y[i]`

## 属性

阶跃函数继承自 Curve，因此拥有 Curve 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线 |
| `visible` | Boolean | true | 是否可见 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |

## 方法

阶跃函数继承自 Curve，因此拥有 Curve 的所有方法：

| 方法 | 参数 | 描述 |
|------|------|------|
| `X()` | 无 | 获取 x 坐标数组 |
| `Y()` | 无 | 获取 y 坐标数组 |
| `updateDataArray()` | 无 | 更新数据数组 |

## 示例

### 1. 基本阶跃函数

```js
// 创建简单的阶跃函数
step = stepfunction(
    [0, 1, 2, 3, 4, 5],
    [1, 3, 0, 2, 2, 1]
);
```

### 2. 设置样式

```js
// 蓝色粗线阶跃函数
step1 = stepfunction(
    [0, 1, 2, 3, 4],
    [0, 1, 2, 1, 0]
) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 虚线阶跃函数
step2 = stepfunction(
    [0, 1, 2, 3, 4],
    [2, 1, 3, 2, 4]
) <<
    dash: 1,
    strokeColor: 'red'
>>;
```

### 3. 动态阶跃函数

```js
// 使用滑块控制阶跃高度
h = slider(0, 5, 0.1);

// 阶跃高度随滑块变化
step = stepfunction(
    [0, 1, 2, 3],
    [0, function() { return V(h); }, 2, 1]
);
```

### 4. 累积分布函数

```js
// 模拟离散随机变量的累积分布函数
// 假设概率分布：P(X=1)=0.2, P(X=2)=0.3, P(X=3)=0.5
cdf = stepfunction(
    [0, 1, 2, 3],
    [0, 0.2, 0.5, 1]
) <<
    strokeColor: 'green',
    strokeWidth: 2
>>;

// 标记点
p1 = point(1, 0.2) << face: 'circle', size: 4 >>;
p2 = point(2, 0.5) << face: 'circle', size: 4 >>;
p3 = point(3, 1) << face: 'circle', size: 4 >>;
```

### 5. 数字信号

```js
// 模拟数字信号（方波）
digitalSignal = stepfunction(
    [0, 1, 2, 3, 4, 5, 6, 7, 8],
    [0, 1, 0, 1, 0, 1, 0, 1, 0]
) <<
    strokeColor: 'black',
    strokeWidth: 2
>>;
```

### 6. 税率阶梯

```js
// 模拟累进税率
// 收入区间和对应税率
taxRate = stepfunction(
    [0, 50000, 100000, 200000, 500000],
    [0, 0.1, 0.2, 0.3, 0.35]
) <<
    strokeColor: 'purple',
    strokeWidth: 2
>>;

// 标记税率变化点
t1 = point(50000, 0.1) << face: '[]', size: 5 >>;
t2 = point(100000, 0.2) << face: '[]', size: 5 >>;
t3 = point(200000, 0.3) << face: '[]', size: 5 >>;
```

### 7. 与函数图像对比

```js
// 原函数
f = functiongraph(
    function(x) { return x * x; },
    -3, 3
) << strokeColor: 'blue' >>;

// 阶梯近似
stepApprox = stepfunction(
    [-3, -2, -1, 0, 1, 2, 3],
    [9, 4, 1, 0, 1, 4, 9]
) << strokeColor: 'red', dash: 1 >>;
```

### 8. 更新数据

```js
// 创建阶跃函数
step = stepfunction(
    [0, 1, 2, 3],
    [0, 1, 2, 3]
);

// 在代码中可以通过以下方式更新数据
// step.updateDataArray();
// step.xTerm = [0, 1, 2, 3, 4];
// step.yTerm = [0, 2, 1, 3, 2];
```

### 9. 分段常数逼近

```js
// 用阶跃函数逼近正弦函数
// 将区间 [-π, π] 分成 8 段
n = 8;
xVals = [];
yVals = [];

for (i = 0; i <= n; i = i + 1) {
    xVals[i] = -PI + (2 * PI * i) / n;
    if (i < n) {
        yVals[i] = sin(xVals[i]);
    }
}

stepSine = stepfunction(xVals, yVals) <<
    strokeColor: 'orange',
    strokeWidth: 2
>>;

// 原正弦函数对比
sinGraph = functiongraph(sin, -PI, PI) <<
    strokeColor: 'blue',
    dash: 1
>>;
```

### 10. 电费阶梯计价

```js
// 居民用电阶梯电价
// 0-180 度：0.5 元/度
// 181-260 度：0.6 元/度
// 261-400 度：0.8 元/度
// 400 度以上：1.0 元/度
electricityPrice = stepfunction(
    [0, 180, 260, 400, 600],
    [0.5, 0.6, 0.8, 1.0, 1.0]
) <<
    strokeColor: 'red',
    strokeWidth: 3
>>;
```

## 注意事项

1. **数据点更新**：如果需要在创建后更新数据点，可以通过 `xTerm` 和 `yTerm` 属性访问和修改
2. **区间定义**：阶跃函数在每个区间 `[x[i], x[i+1])` 上取值为 `y[i]`
3. **数组长度**：x 数组和 y 数组必须有相同的长度
4. **继承属性**：阶跃函数继承自 Curve，可以使用 Curve 的所有属性进行样式设置
5. **与 Functiongraph 的区别**：阶跃函数是分段常数，而函数图像是连续的

## 相关元素

- [Curve](./Curve.md) - 曲线（父类）
- [Functiongraph](./Functiongraph.md) - 函数图像
- [Slider](./Slider.md) - 滑块（控制动态参数）
