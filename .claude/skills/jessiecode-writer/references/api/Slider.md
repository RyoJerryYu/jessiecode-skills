# Slider 滑块

## 描述

滑块用于在给定范围内选择数值。滑块是滑点 (Glider) 的一种特殊形式。

## JessieCode 语法

```js
// 基本语法
s = slider(start, end, range);

// 带属性创建
s = slider(start, end, range) <<
    withLabel: true,
    name: 'a',
    snapWidth: 0.1
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| start | Array | 滑块起点坐标 `[x, y]` |
| end | Array | 滑块终点坐标 `[x, y]` |
| range | Array | 数值范围 `[min, start, max]` |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `withLabel` | Boolean | true | 是否显示标签 |
| `withTicks` | Boolean | true | 是否显示刻度 |
| `name` | String | '' | 滑块名称 |
| `snapWidth` | Number | -1 | 步长（-1 表示连续） |
| `digits` | Number | 2 | 显示的小数位数 |
| `size` | Number | 6 | 滑块点的大小 |
| `moveOnUp` | Boolean | true | 点击基线移动滑块 |
| `suffixLabel` | String | null | 标签前缀（替代 "name = "） |
| `unitLabel` | String | null | 单位标签 |
| `postLabel` | String | null | 标签后缀 |

### 子元素属性

| 子元素 | 描述 |
|--------|------|
| `baseline` | 基线属性 |
| `highline` | 高亮线属性 |
| `point1` | 起点属性 |
| `point2` | 终点属性 |
| `ticks` | 刻度属性 |
| `label` | 标签属性 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `Value()` | 无 | 获取当前值 |
| `setValue(val)` | val: Number | 设置值（需调用 `$board.update()`） |
| `setMin(val)` | val: Number | 设置最小值 |
| `setMax(val)` | val: Number | 设置最大值 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `V(slider)` | 获取滑块值 | `V(s)` |

## 示例

### 1. 创建基本滑块

```js
// 范围 1 到 10，初始值 5
s = slider([1, 2], [3, 2], [1, 5, 10]);

// 使用滑块控制圆的半径
O = point(0, 0);
c = circle(O, function() { return V(s); });
```

### 2. 设置步长（离散值）

```js
// 整数滑块
s1 = slider([1, 3], [3, 1], [0, 3, 5]) <<
    snapWidth: 1
>>;

// 步长为 0.5
s2 = slider([1, 2], [3, 2], [0, 1, 5]) <<
    snapWidth: 0.5
>>;

// 连续滑块（默认）
s3 = slider([1, 1], [3, 1], [-5, 0, 5]);
```

### 3. 自定义标签

```js
// 自定义前缀和单位
s = slider([-3, 1], [1, 1], [-10, 1, 10]) <<
    name: 'xyz',
    suffixLabel: 'x = ',
    unitLabel: ' m',
    postLabel: '',
    label: << fontSize: 16 >>
>>;

// 仅显示值（无名称）
s2 = slider([-3, 2], [1, 2], [0, 0.5, 1]) <<
    withLabel: true,
    name: '',
    suffixLabel: ''
>>;
```

### 4. 设置颜色

```js
s = slider([-3, 1], [1, 1], [-10, 1, 10]) <<
    baseline: << strokeColor: 'blue' >>,
    highline: << strokeColor: 'red' >>,
    fillColor: 'yellow',
    label: << strokeColor: 'orange', fontSize: 18 >>
>>;
```

### 5. 使用滑块值

```js
// 创建滑块
a = slider([1, 4], [4, 4], [0, 1, 5]);

// 方法 1：使用 V() 函数
P1 = point(function() { return V(a); }, 0);

// 方法 2：直接使用 Value() 方法
// P2 = point(function() { return a.Value(); }, 1);

// 显示值
text(1, 3, "a = " + V(a));
```

### 6. 滑块控制多个对象

```js
// 一个滑块控制多个图形
r = slider([1, 4], [4, 4], [0.5, 2, 4]);

// 同心圆
O = point(0, 0);
c1 = circle(O, function() { return V(r); });
c2 = circle(O, function() { return V(r) * 0.5; });
c3 = circle(O, function() { return V(r) * 1.5; });

// 正多边形顶点
for (i = 0; i < 6; i = i + 1) {
    angle = i * PI / 3;
    point(function() { return cos(angle) * V(r); },
          function() { return sin(angle) * V(r); });
}
```

### 7. 动态滑块（可拖动位置）

```js
// 可拖动端点的滑块
s = slider([-3, 1], [2, 1], [-10, 1, 10]) <<
    point1: << fixed: false >>,
    point2: << fixed: false >>,
    baseline: << fixed: false >>
>>;
```

### 8. 滑块动画

```js
// 创建滑块
s = slider([1, 2], [4, 2], [0, 0, 10]);

// 启动动画：方向 1（向右），20 步，30ms 间隔，2 圈
// 注意：JessieCode 中动画可能需要通过按钮触发
// s.startAnimation(1, 20, 30, 2);

// 更常用的方式是使用函数创建动态点
t = slider([1, 3], [4, 3], [0, 0, 2*PI]);
P = point(function() { return cos(V(t)); },
          function() { return sin(V(t)); });
```

### 9. 分数显示

```js
// 使用 MathJax 显示分数标签（需要加载 MathJax）
s = slider([-3, 2], [2, 2], [-10, 1, 10]) <<
    name: 'A',
    suffixLabel: '\\(A = ',
    postLabel: '\\)',
    label: << useMathJax: true >>
>>;
```

### 10. 滑块组合使用

```js
// 多个滑块控制不同参数
a = slider([-4, 4], [-1, 4], [-5, 1, 5]) << name: 'a' >>;
b = slider([-4, 3.5], [-1, 3.5], [-5, 2, 5]) << name: 'b' >>;
c = slider([-4, 3], [-1, 3], [-5, -1, 5]) << name: 'c' >>;

// 二次函数 f(x) = ax² + bx + c
f = function(x) {
    return V(a) * x * x + V(b) * x + V(c);
};

// 绘制函数图像
graph = functiongraph(f, -5, 5);
```

## 注意事项

1. **范围数组**：`range` 参数格式为 `[min, start, max]`，分别表示最小值、初始值、最大值
2. **步长**：`snapWidth` 设置为正数时，滑块只返回该值的整数倍；设置为 -1 时为连续值
3. **获取值**：使用 `V(slider)` 函数或 `slider.Value()` 方法获取当前值
4. **更新**：使用 `setValue()` 设置值后，需要调用 `$board.update()` 更新画布
5. **标签格式**：默认显示格式为 "name = value"，可使用 `suffixLabel` 自定义

## 相关元素

- [Glider](./Glider.md) - 滑点
- [Button](./Button.md) - 按钮（可用于控制滑块动画）
- [Ticks](./Ticks.md) - 刻度
