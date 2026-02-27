# Chart 图表

<!-- USAGE_FREQUENCY: advanced -->

## 描述

图表元素用于数据可视化，支持多种图表类型：柱状图 (bar)、拟合图 (fit)、折线图 (line)、饼图 (pie)、点图 (point)、雷达图 (radar)、样条曲线图 (spline)。

## JessieCode 语法

```js
// 基本语法 - 创建柱状图
chart = chart([y0, y1, y2, ...]) <<
    chartStyle: 'bar',
    width: 0.8,
    labels: ['A', 'B', 'C', 'D']
>>;

// 带 x 坐标的图表
chart = chart([x0, x1, x2, ...], [y0, y1, y2, ...]) <<
    chartStyle: 'line,point'
>>;

// 饼图
chart = chart([v0, v1, v2, ...]) <<
    chartStyle: 'pie',
    center: [5, 2],
    colors: ['#B02B2C', '#3F4C6B', '#C79810']
>>;

// 雷达图
chart = chart([[v00, v01], [v10, v11], ...]) <<
    chartStyle: 'radar',
    paramArray: ['Speed', 'Flexibility', 'Costs'],
    labelArray: ['Ruby', 'JavaScript', 'PHP']
>>;

// 使用函数创建动态图表
chart = chart([function() { return slider1.Value(); }, ...]) <<
    chartStyle: 'bar'
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Array | x 坐标数组（可选，默认 [1, 2, 3, ...]） |
| y | Array | y 坐标数组或嵌套数组 `[[x0,x1,...],[y0,y1,...]]` |

### 父数组格式

图表元素的父数组可以是以下形式之一：

1. **简单数组** `[number, number, number, ...]`：解释为 y 坐标数组，x 坐标自动设置为 `[1, 2, 3, ...]`
2. **嵌套数组** `[[number, number, ...]]`：内容解释为 y 坐标数组，x 坐标自动设置
3. **完整格式** `[[x0,x1,x2,...],[y0,y1,y2,...]]`：同时指定 x 和 y 坐标

## 属性

### 通用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `chartStyle` | String | 'bar' | 图表类型：'bar', 'fit', 'line', 'pie', 'point', 'radar', 'spline' |
| `width` | Number | 0.8 | 柱状图宽度（相对单位） |
| `labels` | Array | [] | 数据标签数组 |
| `colorArray` | Array | 默认颜色数组 | 颜色数组 |
| `fillOpacity` | Number | 0.7 | 填充透明度 (0-1) |
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 1 | 描边宽度 |
| `center` | Array | [0, 0] | 饼图中心坐标 |
| `visible` | Boolean | true | 是否可见 |

### 标签属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `label` | Object | {} | 标签配置对象 |
| `labelArray` | Array | [] | 系列标签数组（雷达图） |
| `paramArray` | Array | [] | 参数轴标签数组（雷达图） |

### 标签配置对象属性

```js
label: {
    fontSize: 30,
    display: 'internal',
    anchorX: 'left',
    rotate: 90
}
```

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `fontSize` | Number | 14 | 字体大小 |
| `display` | String | 'external' | 显示位置：'internal' 或 'external' |
| `anchorX` | String | 'center' | 水平锚点：'left', 'center', 'right' |
| `rotate` | Number | 0 | 旋转角度（度） |

### 雷达图特有属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `legendPosition` | String | 'right' | 图例位置 |
| `startAngle` | Number | Math.PI/2 | 起始角度 |
| `radius` | Number | 自动 | 雷达图半径 |
| `showCircles` | Boolean | true | 是否显示辅助圆 |
| `circleLabelArray` | Array | [] | 辅助圆标签 |
| `highlightColorArray` | Array | [] | 高亮颜色数组 |

### 高亮属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `highlightBySize` | Boolean | false | 是否通过大小区分高亮 |
| `highlightOnSector` | Boolean | false | 是否在扇区上高亮 |

## 方法

图表元素返回的是一个数组，包含多个子元素。可以通过索引访问：

```js
// 对于折线 + 点图
chart = chart(data) << chartStyle: 'line,point' >>;
lineElement = chart[0];   // 折线元素
pointArray = chart[1];    // 点数组

// 设置属性
chart[0].setAttribute('strokeColor: blue');
for (var i = 0; i < pointArray.length; i++) {
    pointArray[i].setAttribute({strokeColor: 'red', size: 5});
}
```

## 示例

### 1. 创建基本柱状图

```js
// 简单柱状图
data = [4, 2, -1, 3, 6, 7, 2];
chart = chart(data) <<
    chartStyle: 'bar',
    width: 0.8,
    labels: data,
    colorArray: ['#8E1B77', '#BE1679', '#DC1765', '#DA2130', '#DB311B']
>>;
```

### 2. 设置标签样式

```js
data = [4, 2, 6, 3, 7];
chart = chart(data) <<
    chartStyle: 'bar',
    labels: data,
    label: <<
        fontSize: 30,
        display: 'internal',
        anchorX: 'left',
        rotate: 90
    >>
>>;
```

### 3. 动态图表（使用滑块）

```js
// 创建滑块
s = slider(1, 2, 0.1) << name: 'S' >>;

// 动态数据
data = [
    function() { return s.Value() * 4.5; },
    function() { return s.Value() * (-1); },
    function() { return s.Value() * 3; },
    function() { return s.Value() * 2; },
    function() { return s.Value() * 5.5; }
];

chart = chart(data) <<
    chartStyle: 'bar',
    width: 0.8,
    labels: data,
    colorArray: ['#8E1B77', '#BE1679', '#DC1765', '#DA2130', '#DB311B']
>>;
```

### 4. 折线图 + 点图

```js
// 组合图表：折线 + 点
dataArr = [4, 1, 3, 2, 5, 6.5, 1.5, 2, 0.5, 1.5, -1];
chart = chart(dataArr) <<
    chartStyle: 'line,point'
>>;

// 设置折线属性
chart[0].setAttribute('strokeColor: black, strokeWidth: 2');

// 设置点属性
points = chart[1];
for (var i = 0; i < points.length; i++) {
    points[i].setAttribute({
        strokeColor: 'black',
        fillColor: 'white',
        face: '[]',
        size: 4
    });
}
```

### 5. 饼图

```js
// 创建饼图
dataArr = [4, 1.2, 3, 7, 5, 4, 1.54, 2];
chart = chart(dataArr) <<
    chartStyle: 'pie',
    colors: ['#B02B2C', '#3F4C6B', '#C79810', '#D15600'],
    fillOpacity: 0.9,
    center: [5, 2],
    strokeColor: '#ffffff',
    strokeWidth: 6,
    highlightBySize: true,
    highlightOnSector: true
>>;
```

### 6. 雷达图

```js
// 雷达图数据
dataArr = [
    [23, 14, 15.0],
    [60, 8, 25.0],
    [0, 11.0, 25.0],
    [10, 15, 20.0]
];

chart = chart(dataArr) <<
    chartStyle: 'radar',
    colorArray: ['#0F408D', '#6F1B75', '#CA147A', '#DA2228', '#E8801B'],
    paramArray: ['Speed', 'Flexibility', 'Costs'],
    labelArray: ['Ruby', 'JavaScript', 'PHP', 'Python'],
    legendPosition: 'right',
    start: 0
>>;
```

### 7. 带坐标的图表

```js
// 指定 x 和 y 坐标
xData = [1, 2, 3, 4, 5];
yData = [2, 4, 1, 5, 3];

chart = chart(xData, yData) <<
    chartStyle: 'spline',
    strokeColor: 'blue',
    strokeWidth: 2
>>;
```

## 注意事项

1. **图表类型**：`chartStyle` 可以是多个类型的组合，用逗号分隔，如 `'line,point'`
2. **返回值**：图表元素返回的是数组，组合图表包含多个子元素
3. **动态更新**：使用函数作为数据值可以实现动态更新
4. **颜色数组**：`colorArray` 中的颜色会循环应用到数据系列
5. **饼图中心**：使用 `center` 属性设置饼图的中心位置
6. **雷达图标签**：使用 `labelArray` 设置系列名称，`paramArray` 设置参数轴名称

## 相关元素

- [Slider](./Slider.md) - 滑块（用于创建动态图表）
- [Point](./Point.md) - 点（图表中的数据点）
- [Line](./Line.md) - 线（折线图的线条）
- [Board](./Board.md) - 画板（图表容器）
