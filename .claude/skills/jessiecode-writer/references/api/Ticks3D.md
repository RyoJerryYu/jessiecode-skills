# Ticks3D 3D 刻度

<!-- USAGE_FREQUENCY: advanced -->

## 描述

刻度用于在 3D 视图中作为直线上的距离标记。

## JessieCode 语法

```js
// 在 3D 直线上创建刻度
ticks = view.create('ticks3d', [point, direction1, length, direction2], options);

// 带属性创建
ticks = view.create('ticks3d', [point, dir1, len, dir2], <<
    ticksDistance: 2,
    majorHeight: 10,
    drawLabels: true
>>);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| point | Array/Function | 长度为 3 的数组，确定刻度的起始点 |
| direction1 | Array/Function | 长度为 3 的数组，3D 直线的方向 |
| length | Number/Function | 直线的长度 |
| direction2 | Array/Function | 长度为 3 的数组，刻度的方向 |

**参数说明**：
- `point` 是长度为 3 的数组，确定网格的起始点
- `direction1` 和 `direction2` 是长度为 3 的数组
- `direction1` 是 3D 直线的方向
- `direction2` 是刻度的方向
- `length` 是直线的长度
- 所有参数可以作为函数提供，返回适当的数据类型
- 刻度的间距由属性 `ticksDistance` 确定

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `ticksDistance` | Number | 1 | 主刻度间距（用户坐标） |
| `majorHeight` | Number | 10 | 主刻度高度（像素） |
| `minorHeight` | Number | 4 | 次刻度高度（像素） |
| `minorTicks` | Number | 4 | 主刻度间的次刻度数量 |
| `drawLabels` | Boolean | false | 是否显示刻度标签 |
| `drawZero` | Boolean | false | 是否显示零刻度 |
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 1 | 线宽（像素） |
| `visible` | Boolean | true | 是否可见 |

### 标签属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `label.fontSize` | Number | 12 | 标签字体大小 |
| `label.strokeColor` | String | '#000000' | 标签颜色 |
| `label.anchorX` | String | 'middle' | 水平锚点 |
| `label.anchorY` | String | 'middle' | 垂直锚点 |
| `label.offset` | Array | [0, 0] | 标签偏移量 |
| `label.digits` | Number | 2 | 小数位数 |
| `label.useMathJax` | Boolean | false | 使用 MathJax 渲染 |

## 示例

### 1. 基本 3D 刻度

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]],
    {
        projection: 'central'
    });

// 创建 3D 直线
var point = [0, 0, 0];
var direction1 = [1, 0, 0];  // x 轴方向
var direction2 = [0, 0, 1];  // z 轴方向（刻度向上）
var length = 5;

// 创建刻度
var ticks = view.create('ticks3d', [point, direction1, length, direction2], {
    ticksDistance: 1,
    majorHeight: 10,
    strokeColor: 'black'
});
```

### 2. 带标签的刻度

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 沿 x 轴的刻度
var ticks = view.create('ticks3d', [
    [0, 0, 0],      // 起点
    [1, 0, 0],      // 方向
    5,              // 长度
    [0, 0, 1]       // 刻度方向
], {
    ticksDistance: 1,
    majorHeight: 15,
    drawLabels: true,
    label: {
        fontSize: 12,
        anchorX: 'middle',
        anchorY: 'top',
        offset: [0, -5]
    }
});
```

### 3. 次刻度

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 带次刻度的刻度
var ticks = view.create('ticks3d', [
    [0, 0, 0],
    [1, 0, 0],
    5,
    [0, 0, 1]
], {
    ticksDistance: 1,
    majorHeight: 20,
    minorHeight: 10,
    minorTicks: 4,  // 每个主刻度间 4 个次刻度
    drawLabels: true
});
```

### 4. 动态刻度

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 创建滑块
var slider = board.create('slider', [[-4, 4], [4, 4], [0.5, 1, 3]]);

// 动态刻度间距
var ticks = view.create('ticks3d', [
    [0, 0, 0],
    [1, 0, 0],
    5,
    [0, 0, 1]
], {
    ticksDistance: function() { return slider.Value(); },
    majorHeight: 15,
    drawLabels: true
});
```

### 5. 不同方向的刻度

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// x 轴刻度
var ticksX = view.create('ticks3d', [
    [0, 0, 0],
    [1, 0, 0],  // x 方向
    5,
    [0, 0, 1]   // 向上
], {
    ticksDistance: 1,
    majorHeight: 10,
    drawLabels: true,
    label: { strokeColor: 'red' }
});

// y 轴刻度
var ticksY = view.create('ticks3d', [
    [0, 0, 0],
    [0, 1, 0],  // y 方向
    5,
    [0, 0, 1]   // 向上
], {
    ticksDistance: 1,
    majorHeight: 10,
    drawLabels: true,
    label: { strokeColor: 'green' }
});

// z 轴刻度
var ticksZ = view.create('ticks3d', [
    [0, 0, 0],
    [0, 0, 1],  // z 方向
    5,
    [1, 0, 0]   // 向右
], {
    ticksDistance: 1,
    majorHeight: 10,
    drawLabels: true,
    label: { strokeColor: 'blue' }
});
```

### 6. 刻度样式

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 粗刻度线
var ticks1 = view.create('ticks3d', [
    [0, 0, 0], [1, 0, 0], 5, [0, 0, 1]
], {
    ticksDistance: 1,
    majorHeight: 20,
    strokeWidth: 3,
    strokeColor: 'black'
});

// 细刻度线
var ticks2 = view.create('ticks3d', [
    [0, 2, 0], [1, 0, 0], 5, [0, 0, 1]
], {
    ticksDistance: 1,
    majorHeight: 20,
    strokeWidth: 1,
    strokeColor: 'gray'
});
```

### 7. 不显示零刻度

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 不显示零刻度
var ticks = view.create('ticks3d', [
    [-3, 0, 0],
    [1, 0, 0],
    6,
    [0, 0, 1]
], {
    ticksDistance: 1,
    majorHeight: 15,
    drawLabels: true,
    drawZero: false  // 不显示 0 刻度标签
});
```

### 8. 自定义标签格式

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]]);

// 使用 MathJax 显示分数标签
var ticks = view.create('ticks3d', [
    [0, 0, 0],
    [1, 0, 0],
    4,
    [0, 0, 1]
], {
    ticksDistance: 0.5,
    majorHeight: 15,
    drawLabels: true,
    label: {
        digits: 1,
        useMathJax: true,
        anchorX: 'middle',
        anchorY: 'top'
    }
});
```

### 9. 3D 坐标轴刻度

```js
var view = board.create('view3d',
    [[-4, -3], [8, 8],
    [[-5, 5], [-5, 5], [-5, 5]]],
    {
        axesPosition: 'none'
    });

// 创建坐标轴
var xAxis = view.create('line3d',
    [[-5, 0, 0], [5, 0, 0]],
    { strokeColor: 'black', lastArrow: true }
);

var yAxis = view.create('line3d',
    [[0, -5, 0], [0, 5, 0]],
    { strokeColor: 'black', lastArrow: true }
);

var zAxis = view.create('line3d',
    [[0, 0, -5], [0, 0, 5]],
    { strokeColor: 'black', lastArrow: true }
);

// 添加刻度
var ticksX = view.create('ticks3d', [
    [-5, 0, 0], [1, 0, 0], 10, [0, 0, 1]
], {
    ticksDistance: 1,
    majorHeight: 8,
    drawLabels: true
});

var ticksY = view.create('ticks3d', [
    [0, -5, 0], [0, 1, 0], 10, [0, 0, 1]
], {
    ticksDistance: 1,
    majorHeight: 8,
    drawLabels: true
});

var ticksZ = view.create('ticks3d', [
    [0, 0, -5], [0, 0, 1], 10, [1, 0, 0]
], {
    ticksDistance: 1,
    majorHeight: 8,
    drawLabels: true
});
```

## 注意事项

1. **方向向量**：`direction1` 和 `direction2` 应该是单位向量或表示方向的向量
2. **刻度间距**：`ticksDistance` 使用用户坐标，不是像素
3. **刻度高度**：`majorHeight` 和 `minorHeight` 使用像素单位
4. **动态参数**：所有参数都可以是函数，用于创建动态刻度
5. **标签位置**：使用 `label.anchorX`、`label.anchorY` 和 `label.offset` 调整标签位置
6. **3D 投影**：刻度在 3D 空间中的显示效果取决于视图的投影类型（平行或透视）

## 相关元素

- [Line3D](./Line3D.md) - 3D 直线
- [View3D](./View3D.md) - 3D 视图
- [Axis3D](./Axis3D.md) - 3D 坐标轴
- [Ticks](./Ticks.md) - 2D 刻度
