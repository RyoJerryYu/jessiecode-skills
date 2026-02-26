# Legend 图例

## 描述

为图表元素创建图例。参数是一对坐标。标签名称和标签颜色在属性中提供。

## JessieCode 语法

```js
// 基本语法 - 创建图例
legend = legend(x, y);

// 带属性创建
legend = legend(8, 45) <<
    labels: [4, 7, 7, 27, 33, 37],
    colors: ['green', 'yellow', 'red', 'blue'],
    strokeWidth: 5
>>;

// 固定图例（不随缩放移动）
legend = legend(-1.75, 1.75) <<
    labels: [-3, -2, -1, 0, 1, 2, 3],
    colors: ['red'],
    frozen: true
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Number | 图例左上角的水平坐标 |
| y | Number | 图例左上角的垂直坐标 |

## 属性

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `labels` | Array | `['1', '2', '3', '4', '5', '6', '7', '8']` | 图例的标签名称 |
| `colors` | Array | `['#B02B2C', '#3F4C6B', '#C79810', '#D15600', '#FFFF88', '#c3d9ff', '#4096EE', '#008C00']` | 标签颜色（循环）数组 |
| `strokeWidth` | Number | 5 | 图例条目中线的高度（像素） |
| `strokeOpacity` | Array | `[1]` | 图例线描边透明度的（循环）数组 |
| `lineLength` | Number | 1 | 图例条目中线的长度 |
| `rowHeight` | Number | 20 | 每个图例条目的高度（像素） |
| `style` | String | 'vertical' | 图例的默认样式，唯一可能值为 'vertical' |
| `frozen` | Boolean | false | 图例是否固定（不可拖动，缩放时也不移动） |

### 属性说明

**colors** - 标签颜色数组
:   用于图例条目的颜色数组。如果颜色数量少于标签数量，则会循环使用。

**frozen** - 固定图例
:   如果设置为 `true`，图例将被固定，无法拖动。即使在缩放和移动原点事件发生时，图例也会保持在原位置。

**labels** - 标签名称
:   图例元素的标签名称数组。

**lineLength** - 线长度
:   每个图例条目中线的长度。

**rowHeight** - 行高
:   每个图例条目的高度，以像素为单位。

**strokeOpacity** - 描边透明度
:   每个图例条目描边颜色的透明度数组。如果只提供一个值，则应用于所有条目。

**strokeWidth** - 线宽
:   图例条目的线宽，以像素为单位。

**style** - 样式
:   图例的默认样式。唯一可能的值是 'vertical'（垂直）。

## 示例

### 1. 创建基本图例

```js
// 为条形图创建图例
var board = JXG.JSXGraph.initBoard('jxgbox', {
    axis: true,
    boundingbox: [-4, 48.3, 12.0, -2.3]
});

var x = [-3, -2, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8];
var dataArr = [4, 7, 7, 27, 33, 37, 46, 22, 11, 4, 1, 0];
var colors = ['green', 'yellow', 'red', 'blue'];

// 创建条形图
board.create('chart', [x, dataArr], {
    chartStyle: 'bar',
    width: 1.0,
    labels: dataArr,
    colors: colors
});

// 创建图例
board.create('legend', [8, 45], {
    labels: dataArr,
    colors: colors,
    strokeWidth: 5
});
```

### 2. 为隐函数曲线创建图例

```js
// 创建隐函数曲线
var inputFun = "x^2/2-2*x*y+y^2/2";
var niveauline = [-3, -2, -1, -0.5, 0, 1, 2, 3];
var cf = [];
var niveauopac = [];

// 创建多条隐函数曲线
for (let i = 0; i < niveauline.length; i++) {
    let niveaui = niveauline[i];
    niveauopac.push((i + 1) / (niveauline.length + 1));
    cf.push(board.create("implicitcurve", [
        inputFun + "-(" + niveaui.toFixed(2) + ")",
        [-2, 2], [-2, 2]
    ], {
        strokeWidth: 2,
        strokeColor: JXG.palette.red,
        strokeOpacity: niveauopac[i],
        needsRegularUpdate: false,
        name: "niveau" + i,
        visible: true
    }));
}

// 创建图例显示不同层级
legend = board.create('legend', [-1.75, 1.75], {
    labels: niveauline,
    colors: [cf[0].visProp.strokecolor],
    strokeOpacity: niveauopac,
    linelength: 0.2,
    frozen: true
});
```

### 3. 自定义图例样式

```js
// 创建带自定义颜色的图例
legend1 = legend(0, 10) <<
    labels: ['A', 'B', 'C', 'D'],
    colors: ['red', 'blue', 'green', 'orange'],
    strokeWidth: 3,
    lineLength: 2
>>;

// 创建带透明度的图例
legend2 = legend(5, 10) <<
    labels: ['低', '中', '高'],
    colors: ['lightblue', 'blue', 'darkblue'],
    strokeOpacity: [0.3, 0.6, 1.0],
    rowHeight: 25
>>;
```

### 4. 固定图例

```js
// 创建固定图例（不随画布缩放移动）
fixedLegend = legend(-3, 8) <<
    labels: ['系列 1', '系列 2'],
    colors: ['#FF0000', '#00FF00'],
    frozen: true
>>;
```

### 5. JessieCode 语法示例

```js
// 使用 JessieCode 语法创建图例
A = point(1, 1);
B = point(2, 2);

// 创建图表
chart1 = chart([0, 1, 2, 3], [1, 4, 2, 3]) <<
    chartStyle: 'line',
    strokeColor: 'blue'
>>;

// 创建对应的图例
leg1 = legend(4, 4) <<
    labels: ['数据系列'],
    colors: ['blue'],
    strokeWidth: 4
>>;
```

## 注意事项

1. **循环数组**：`colors` 和 `strokeOpacity` 是循环数组。如果标签数量超过数组长度，颜色/透明度会循环使用
2. **固定图例**：设置 `frozen: true` 可使图例固定在画布上的绝对位置，不随缩放和平移移动
3. **坐标位置**：图例的位置由左上角坐标 (x, y) 确定
4. **与 Chart 配合使用**：图例通常与 `chart` 元素配合使用，用于说明图表中不同颜色代表的含义
5. **样式限制**：`style` 属性目前只支持 'vertical'（垂直）样式

## 相关元素

- [Chart](./Chart.md) - 图表
- [Label](./Label.md) - 标签
- [Text](./Text.md) - 文本
- [Slider](./Slider.md) - 滑块
