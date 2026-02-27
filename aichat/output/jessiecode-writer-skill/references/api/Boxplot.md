# Boxplot 箱线图

## 描述

箱线图（Boxplot）用于通过四分位数展示数值数据的分布情况。箱线图可以垂直或水平显示，通过 `dir` 属性控制方向。

## JessieCode 语法

```js
// 基本语法 - 创建垂直箱线图
// [最小值，Q1, 中位数，Q3, 最大值], axis 位置，宽度
box = boxplot([min, q1, median, q3, max], axis, width);

// 创建水平箱线图
box = boxplot([min, q1, median, q3, max], axis, width) <<
    dir: 'horizontal',
    smallWidth: 0.25
>>;

// 带属性创建
box = boxplot([0, 2, 3, 3.5, 5], 0, 3) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    dir: 'vertical'
>>;

// 使用函数创建动态箱线图
box = boxplot([function() { return a; }, 2, 3, 3.5, function() { return b; }], 0, 2);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| quantiles | Array | 包含至少五个四分位数的数组：[最小值，Q1, 中位数，Q3, 最大值] |
| axis | Number/Function | 箱线图的轴位置 |
| width | Number/Function | 箱体部分的宽度 |

### 四分位数数组说明

| 索引 | 名称 | 描述 |
|------|------|------|
| `[0]` | 最小值 | 数据的最小值（下须末端） |
| `[1]` | Q1 | 第一四分位数（25% 分位数，箱体下边界） |
| `[2]` | Q2/中位数 | 中位数（50% 分位数，箱体内线） |
| `[3]` | Q3 | 第三四分位数（75% 分位数，箱体上边界） |
| `[4]` | 最大值 | 数据的最大值（上须末端） |

**注意**：数组元素可以是数字、函数或字符串

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `dir` | String | 'vertical' | 箱线图方向：'vertical'（垂直）或 'horizontal'（水平） |
| `smallWidth` | Number | 0.5 | 最小值和最大值四分位线的相对宽度（相对于箱体宽度） |
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |

### 方向属性 (dir)

| 值 | 描述 | 外观 |
|------|------|------|
| `'vertical'` | 垂直箱线图（默认） | 箱体垂直排列，须向上/下延伸 |
| `'horizontal'` | 水平箱线图 | 箱体水平排列，须向左/右延伸 |

### smallWidth 说明

`smallWidth` 控制最小值和最大值处横线（须末端）的宽度，是相对于箱体宽度的比例：
- `smallWidth: 0.5` - 须末端宽度为箱体宽度的一半（默认）
- `smallWidth: 0.25` - 须末端宽度为箱体宽度的四分之一
- `smallWidth: 0` - 须末端宽度为 0（无横线）

## 示例

### 1. 创建基本垂直箱线图

```js
// 定义四分位数：[最小值，Q1, 中位数，Q3, 最大值]
Q = [-1, 2, 3, 3.5, 5];

// 创建垂直箱线图，位于 x=0 处，宽度为 3
box = boxplot(Q, 0, 3);
```

### 2. 创建水平箱线图

```js
Q = [-1, 2, 3, 3.5, 5];

// 水平箱线图，位于 y=3 处，宽度为 4
box = boxplot(Q, 3, 4) <<
    dir: 'horizontal',
    smallWidth: 0.25,
    strokeColor: 'red'
>>;
```

### 3. 从原始数据计算四分位数

```js
// 原始数据
data = [57, 57, 57, 58, 63, 66, 66, 67, 67, 68, 69, 70, 70, 70, 70, 72, 73, 75, 75, 76, 76, 78, 79, 81];

// 计算四分位数
Q = [];
Q[0] = min(data);  // 最小值
Q[1] = percentile(data, 25);  // Q1
Q[2] = percentile(data, 50);  // 中位数
Q[3] = percentile(data, 75);  // Q3
Q[4] = max(data);  // 最大值

// 创建箱线图
box = boxplot(Q, 0, 3);
```

### 4. 动态箱线图

```js
// 创建滑块控制最小值和最大值
a = slider(-2, 0, 0.1);
b = slider(4, 6, 0.1);

// 使用函数创建动态四分位数
Q = [
    function() { return V(a); },  // 最小值随滑块 a 变化
    2,                              // Q1 固定
    3,                              // 中位数固定
    3.5,                            // Q3 固定
    function() { return V(b); }    // 最大值随滑块 b 变化
];

// 创建动态箱线图
box = boxplot(Q, 0, 2);
```

### 5. 使用滑点控制

```js
// 在 y 轴上创建两个滑点
minPoint = glider(0, -1, axes.y);
maxPoint = glider(0, 5, axes.y);

// 使用滑点的 Y 坐标作为最小值和最大值
Q = [
    function() { return minPoint.Y(); },
    2,
    3,
    3.5,
    function() { return maxPoint.Y(); }
];

// 创建箱线图
box = boxplot(Q, 0, 2);
```

### 6. 多个箱线图对比

```js
// 第一组数据
Q1 = [1, 2, 2.5, 3, 4];
box1 = boxplot(Q1, 0, 2) << strokeColor: 'blue' >>;

// 第二组数据
Q2 = [2, 3, 3.5, 4, 5];
box2 = boxplot(Q2, 3, 2) << strokeColor: 'red' >>;

// 第三组数据
Q3 = [0, 1.5, 2, 2.5, 3];
box3 = boxplot(Q3, 6, 2) << strokeColor: 'green' >>;
```

### 7. 自定义样式

```js
Q = [0, 2, 3, 4, 6];

// 粗线箱线图
box1 = boxplot(Q, 0, 3) <<
    strokeWidth: 5,
    strokeColor: 'purple'
>>;

// 细线箱线图
box2 = boxplot(Q, 4, 3) <<
    strokeWidth: 1,
    strokeColor: 'gray',
    smallWidth: 0.3
>>;
```

## 注意事项

1. **四分位数顺序**：数组必须按从小到大排列：[最小值，Q1, 中位数，Q3, 最大值]
2. **动态更新**：使用函数作为四分位数可以实现动态更新的箱线图
3. **方向选择**：垂直箱线图适合单个分布展示，水平箱线图适合多个分布对比
4. **smallWidth**：设置为 0 可以创建无须末端横线的简化箱线图
5. **数据统计**：可使用 `min()`, `max()`, `percentile()` 等统计函数从原始数据计算四分位数

## 相关元素

- [Slider](./Slider.md) - 滑块（用于动态控制）
- [Glider](./Glider.md) - 滑点（用于动态控制）
- [Statistics](./Statistics.md) - 统计函数（min, max, percentile 等）
