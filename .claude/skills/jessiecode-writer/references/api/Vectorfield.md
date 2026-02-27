# Vectorfield 向量场

<!-- USAGE_FREQUENCY: advanced -->

## 描述

向量场可以可视化为一组带有给定大小和方向的箭头，每个箭头都附着在平面上的一个点上。

绘制向量场可以通过两种方式定义：
- 两个函数 f1(x, y) 和 f2(x, y)
- 一个返回长度为 2 的数组的函数 f(x, y)

## JessieCode 语法

```js
// 基本语法 - 创建向量场
field = vectorfield(F, xData, yData);

// 使用两个函数定义
field = vectorfield([f1, f2], [xStart, xSteps, xEnd], [yStart, ySteps, yEnd]);

// 使用返回数组的函数定义
field = vectorfield(f, [xStart, xSteps, xEnd], [yStart, ySteps, yEnd]);

// 带属性创建
field = vectorfield([f1, f2], [-6, 25, 6], [-5, 20, 5]) <<
    scale: 1,
    arrowHead: <<
        enabled: true,
        size: 8,
        angle: PI / 16
    >>
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| F | Array/Function | 包含两个函数 f1(x, y) 和 f2(x, y) 的数组，或返回长度为 2 的数组的函数 f(x, y) |
| xData | Array | 长度为 3 的数组，包含 x 的起始值、步数、结束值。向量场在 x 方向将包含 (步数) + 1 个向量 |
| yData | Array | 长度为 3 的数组，包含 y 的起始值、步数、结束值。向量场在 y 方向将包含 (步数) + 1 个向量 |

## 属性

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `scale` | Number/Function | 1 | 向量的缩放因子 |
| `arrowHead` | Object | 见下方 | 自定义向量的箭头样式 |
| `strokeColor` | String | '#000000' | 向量线条颜色 |
| `strokeWidth` | Number | 2 | 向量线条宽度 |
| `highlightStrokeColor` | String | 高亮颜色 | 高亮时的颜色 |

### 箭头属性 (arrowHead)

```js
arrowHead: <<
    enabled: true,    // 是否启用箭头
    size: 8,          // 箭头腿的长度（像素）
    angle: PI / 16    // 箭头腿的角度（弧度）
>>
```

| 字段 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `enabled` | Boolean | true | 是否启用箭头 |
| `size` | Number | 5 | 箭头腿的长度（像素） |
| `angle` | Number | π/8 | 箭头腿的角度（弧度） |

**注意**：启用箭头会降低性能。

## 方法

### setF(func)

设置向量场的定义函数。

| 参数 | 类型 | 描述 |
|------|------|------|
| func | Array/Function | 包含两个函数 f1(x, y) 和 f2(x, y) 的数组，或返回长度为 2 的数组的函数 f(x, y) |

**返回值**：向量场对象的引用

## 示例

### 1. 创建基本向量场

```js
// 定义函数
fx = (x, y) => sin(y);
fy = (x, y) => cos(x);

// 创建向量场
field = vectorfield(
    [fx, fy],        // 定义函数
    [-6, 25, 6],     // 水平网格
    [-5, 20, 5]      // 垂直网格
);
```

### 2. 使用滑块控制向量

```js
// 创建滑块控制向量长度
s = slider([-3, 7], [3, 7], [0, 0.33, 1]) << name: 'length' >>;

// 创建滑块控制步数
stepsize = slider([-3, 6], [3, 6], [1, 20, 100]) <<
    name: 'steps',
    snapWidth: 1
>>;

// 定义函数
fx = (x, y) => 0.2 * y;
fy = (x, y) => 0.2 * (cos(x) - 2) * sin(x);

// 创建向量场
field = vectorfield(
    [fx, fy],                    // 定义函数
    [-6, function() { return V(stepsize); }, 6],   // 水平网格
    [-5, function() { return V(stepsize); }, 5]    // 垂直网格
) <<
    highlightStrokeColor: 'blue',  // 设置高亮颜色
    scale: function() { return V(s); },  // 向量缩放
    arrowHead: <<
        enabled: true,
        size: 8,
        angle: PI / 16
    >>
>>;
```

### 3. 使用返回数组的函数

```js
// 定义返回数组的函数
f = (x, y) => [sin(y), cos(x)];

// 创建向量场
field = vectorfield(
    f,
    [-10, 20, 10],
    [-10, 20, 10]
);
```

### 4. 动态更新向量场

```js
// 创建初始向量场
fx = (x, y) => x;
fy = (x, y) => -y;
field = vectorfield([fx, fy], [-5, 10, 5], [-5, 10, 5]);

// 使用 setF 方法更新函数
// 注意：JessieCode 中通常通过重新创建或使用动态函数实现
a = slider(-2, 2, 0.1);
field2 = vectorfield(
    [function(x, y) { return a * x; },
     function(x, y) { return -a * y; }],
    [-5, 10, 5],
    [-5, 10, 5]
);
```

### 5. 不同样式的向量场

```js
// 无箭头的向量场
field1 = vectorfield(
    [(x, y) => y, (x, y) => -x],
    [-5, 15, 5],
    [-5, 15, 5]
) <<
    arrowHead: << enabled: false >>,
    strokeColor: 'gray'
>>;

// 大箭头的向量场
field2 = vectorfield(
    [(x, y) => cos(x), (x, y) => sin(y)],
    [-5, 10, 5],
    [-5, 10, 5]
) <<
    arrowHead: <<
        enabled: true,
        size: 12,
        angle: PI / 8
    >>,
    strokeColor: 'red',
    strokeWidth: 2
>>;
```

### 6. 漩涡向量场

```js
// 创建漩涡向量场
field = vectorfield(
    [(x, y) => -y, (x, y) => x],
    [-5, 20, 5],
    [-5, 20, 5]
) <<
    scale: 0.5,
    arrowHead: <<
        enabled: true,
        size: 6,
        angle: PI / 12
    >>,
    strokeColor: 'blue'
>>;
```

### 7. 鞍点向量场

```js
// 创建鞍点向量场
field = vectorfield(
    [(x, y) => x, (x, y) => -y],
    [-4, 16, 4],
    [-4, 16, 4]
) <<
    scale: 0.8,
    arrowHead: << enabled: true >>,
    strokeColor: 'purple'
>>;
```

## 注意事项

1. **性能**：启用箭头 (`arrowHead.enabled: true`) 会降低渲染性能，特别是在网格点较多时
2. **缩放**：`scale` 属性用于控制向量的显示长度，值为 1 表示原始大小
3. **函数定义**：可以使用两个独立函数或一个返回数组的函数来定义向量场
4. **网格密度**：xData 和 yData 中的步数值决定了向量的密度，步数越多向量越密集
5. **动态更新**：可以通过在参数中使用函数来实现动态更新的向量场

## 相关元素

- [Slopefield](./Slopefield.md) - 斜率场
- [Functiongraph](./Functiongraph.md) - 函数图像
- [Curve](./Curve.md) - 曲线
- [Slider](./Slider.md) - 滑块（用于动态控制）
