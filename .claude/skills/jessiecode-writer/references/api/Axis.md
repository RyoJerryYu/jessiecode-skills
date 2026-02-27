# Axis 坐标轴

<!-- USAGE_FREQUENCY: advanced -->

## 描述

坐标轴是一种带有刻度和标签的直线。它本质上是 [Line](./Line.md) 的包装器，设置了 `straightFirst` 和 `straightLast` 属性为 true，并自动添加箭头和刻度。

## JessieCode 语法

```js
// 基本语法 - 通过两个点创建坐标轴
axis = axis(point1, point2);

// 通过坐标数组创建
axis = axis([x1, y1], [x2, y2]);

// 带属性创建
axis = axis([0, 0], [1, 0]) <<
    withTicks: true,
    ticks: <<
        ticksDistance: 1,
        drawLabels: true
    >>
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| point1 | Point/Array | 轴上的第一个点 |
| point2 | Point/Array | 轴上的第二个点 |

## 属性

坐标轴继承自 Line，因此拥有 Line 的所有属性，并添加了以下特有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `withTicks` | Boolean | true | 是否显示刻度 |
| `ticks` | Object | - | 刻度属性 |
| `position` | String | 'static' | 轴的行为模式 |
| `anchor` | String | '' | 轴的位置锚点 |
| `anchorDist` | String/Number | '10%' | 轴与画布边缘的距离 |
| `label` | Object | - | 轴标签属性 |
| `point1` | Object | - | 第一个点的属性 |
| `point2` | Object | - | 第二个点的属性 |
| `ticksAutoPos` | Boolean | false | 自动调整刻度标签位置 |
| `ticksAutoPosThreshold` | String/Number | '5%' | 自动调整阈值 |

### 位置模式 (position)

| 值 | 描述 |
|----|------|
| `'static'` | 标准行为，轴随画布导航移动 |
| `'fixed'` | 固定在指定位置，不随画布导航移动 |
| `'sticky'` | 混合模式，轴始终保持在可见区域 |

### 锚点方向 (anchor)

| 值 | 描述 |
|----|------|
| `'left'` | 左侧 |
| `'right'` | 右侧 |
| `'left right'` | 左右两侧 |

## 示例

### 1. 创建基本坐标轴

```js
// 创建 x 轴
xAxis = axis([0, 0], [1, 0]);

// 创建 y 轴
yAxis = axis([0, 0], [0, 1]);
```

### 2. 设置刻度

```js
// x 轴带刻度
xAxis = axis([0, 0], [1, 0]) <<
    withTicks: true,
    ticks: <<
        ticksDistance: 1,
        majorHeight: 10,
        minorTicks: 4,
        drawLabels: true
    >>
>>;

// y 轴带刻度
yAxis = axis([0, 0], [0, 1]) <<
    ticks: <<
        ticksDistance: 1,
        drawLabels: true
    >>
>>;
```

### 3. 自定义刻度标签

```js
// 分数标签
xAxis = axis([0, 0], [1, 0]) <<
    ticks: <<
        label: <<
            toFraction: true,
            useMathjax: true,
            anchorX: 'middle',
            offset: [0, -10]
        >>
    >>
>>;

// 自定义小数位数
yAxis = axis([0, 0], [0, 1]) <<
    ticks: <<
        label: <<
            digits: 2
        >>
    >>
>>;
```

### 4. 固定坐标轴

```js
// 固定在画布边缘
xAxis = axis([0, 0], [1, 0]) <<
    position: 'fixed',
    anchor: 'bottom',
    anchorDist: '10%'
>>;

// 粘性坐标轴（始终可见）
yAxis = axis([0, 0], [0, 1]) <<
    position: 'sticky',
    anchor: 'left',
    anchorDist: '10%'
>>;
```

### 5. 自动调整刻度位置

```js
// 自动将刻度标签放置在较窄的一侧
axis = axis([0, 0], [1, 0]) <<
    ticksAutoPos: true,
    ticksAutoPosThreshold: '5%',
    ticks: <<
        ticksDistance: 1,
        drawLabels: true
    >>
>>;
```

### 6. 自定义轴标签

```js
// x 轴标签
xAxis = axis([0, 0], [1, 0]) <<
    label: <<
        text: 'x',
        fontSize: 14,
        offset: [0, 20]
    >>
>>;

// y 轴标签
yAxis = axis([0, 0], [0, 1]) <<
    label: <<
        text: 'y',
        fontSize: 14,
        offset: [-20, 0]
    >>
>>;
```

### 7. 隐藏刻度

```js
// 无刻度坐标轴
axis = axis([0, 0], [1, 0]) <<
    withTicks: false
>>;

// 或
axis = axis([0, 0], [1, 0]) <<
    ticks: << visible: false >>
>>;
```

### 8. 标准坐标系

```js
// 创建标准直角坐标系
xAxis = axis([-5, 0], [5, 0]) <<
    ticks: <<
        ticksDistance: 1,
        majorHeight: 10,
        minorTicks: 4,
        drawLabels: true,
        label: << fontSize: 11 >>
    >>,
    label: << text: 'x', offset: [0, 20] >>
>>;

yAxis = axis([0, -5], [0, 5]) <<
    ticks: <<
        ticksDistance: 1,
        majorHeight: 10,
        drawLabels: true
    >>,
    label: << text: 'y', offset: [-20, 0] >>
>>;
```

### 9. 极坐标轴

```js
// 极坐标角度轴
angleAxis = axis([0, 0], [1, 0]) <<
    ticks: <<
        type: 'polar',
        ticksDistance: PI/4,
        drawLabels: true,
        label: <<
            toFraction: true,
            useMathjax: true
        >>
    >>
>>;
```

### 10. 组合使用

```js
// 完整的坐标系示例
// x 轴
xAxis = axis([-6, 0], [6, 0]) <<
    strokeColor: 'black',
    strokeWidth: 2,
    lastArrow: true,
    ticks: <<
        ticksDistance: 1,
        majorHeight: 10,
        minorTicks: 4,
        drawLabels: true,
        label: <<
            fontSize: 10,
            offset: [0, 15]
        >>
    >>,
    label: <<
        text: 'x',
        fontSize: 14,
        offset: [0, 25]
    >>
>>;

// y 轴
yAxis = axis([0, -6], [0, 6]) <<
    strokeColor: 'black',
    strokeWidth: 2,
    lastArrow: true,
    ticks: <<
        ticksDistance: 1,
        majorHeight: 10,
        drawLabels: true
    >>,
    label: <<
        text: 'y',
        fontSize: 14,
        offset: [-25, 0]
    >>
>>;
```

## 注意事项

1. **自动刻度**：坐标轴默认自动创建刻度，可通过 `withTicks: false` 禁用
2. **方向**：坐标轴会自动延伸到画布边界
3. **箭头**：坐标轴默认在末端显示箭头
4. **水平/垂直**：`position` 属性仅对严格水平或垂直的轴有效
5. **刻度属性**：可以通过 `ticks` 属性对象自定义所有刻度相关设置

## 相关元素

- [Line](./Line.md) - 直线（坐标轴的基类）
- [Ticks](./Ticks.md) - 刻度
- [Grid](./Grid.md) - 网格
