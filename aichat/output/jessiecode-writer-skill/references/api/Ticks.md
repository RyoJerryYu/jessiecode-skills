# Ticks 刻度

## 描述

刻度用于在直线或曲线上标记距离。主要用于坐标轴和滑块元素。刻度可以无限延伸或有限延伸，可以通过 `majorHeight` 和 `minorHeight` 属性控制。

## JessieCode 语法

```js
// 在直线上创建刻度
ticks = ticks(line);

// 带属性创建
ticks = ticks(l) <<
    ticksDistance: 2,
    majorHeight: 40,
    drawLabels: true
>>;

// 在创建坐标轴时自动包含刻度
axis = axis(point1, point2, options);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| line | Line/Curve | 刻度依附的直线或曲线 |
| ticks (可选) | Array | 刻度位置数组或刻度距离 |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `ticksDistance` | Number | 1 | 主刻度间距（用户坐标） |
| `majorHeight` | Number | 10 | 主刻度高度（像素），负数表示全高 |
| `minorHeight` | Number | 4 | 次刻度高度（像素） |
| `minorTicks` | Number | 4 | 主刻度间的次刻度数量 |
| `drawLabels` | Boolean | false | 是否显示刻度标签 |
| `drawZero` | Boolean | false | 是否显示零刻度 |
| `anchor` | String | 'left' | 零刻度位置：'left', 'middle', 'right' 或数字 |
| `insertTicks` | Boolean | false | 自动计算刻度间距 |
| `minTicksDistance` | Number | 10 | 最小刻度间距（像素） |
| `label` | Object | - | 标签属性 |
| `scale` | Number | 1 | 刻度缩放比例 |

### 标签相关属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `digits` | Number | 2/3 | 小数位数 |
| `maxLabelLength` | Number | 5 | 标签最大字符数 |
| `toFraction` | Boolean | false | 显示为分数 |
| `useMathJax` | Boolean | false | 使用 MathJax 渲染 |
| `beautifulScientificTickLabels` | Boolean | false | 美化科学计数法 |

### 刻度方向

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `tickEndings` | Array | [1, 1] | 次刻度方向 |
| `majorTickEndings` | Array | [1, 1] | 主刻度方向 |
| `ignoreInfiniteTickEndings` | Boolean | true | 忽略无限刻度方向 |

**方向说明**：
- `[0, 1]`：仅右侧可见
- `[1, 0]`：仅左侧可见
- `[1, 1]`：两侧可见
- `[0, 0]`：不可见

## 示例

### 1. 基本刻度

```js
// 创建直线
p1 = point(0, 3);
p2 = point(1, 3);
l1 = line(p1, p2);

// 创建刻度
t = ticks(l1) <<
    ticksDistance: 2,
    majorHeight: 40
>>;
```

### 2. 带标签的刻度

```js
// 创建刻度及标签
t = ticks(l1) <<
    ticksDistance: 1,
    drawLabels: true,
    majorHeight: 20,
    minorTicks: 4
>>;
```

### 3. 分数刻度标签

```js
// 使用分数显示刻度
axis = axis([0, 1], [1, 1]) <<
    ticks: <<
        label: <<
            toFraction: true,
            useMathjax: true,
            display: 'html',
            anchorX: 'middle',
            offset: [0, -10]
        >>
    >>
>>;
```

### 4. 自定义刻度位置

```js
// 在特定位置创建刻度
t = ticks(l1, [0, 1, 3, 6, 10]) <<
    majorHeight: 30,
    drawLabels: true
>>;
```

### 5. 自动刻度间距

```js
// 让 JSXGraph 自动计算刻度间距
t = ticks(l1) <<
    insertTicks: true,
    minTicksDistance: 50  // 最小 50 像素间距
>>;
```

### 6. 刻度锚点位置

```js
// 零刻度在左侧（默认）
t1 = ticks(l1) << anchor: 'left' >>;

// 零刻度在中间
t2 = ticks(l1) << anchor: 'middle' >>;

// 零刻度在右侧
t3 = ticks(l1) << anchor: 'right' >>;

// 零刻度在指定坐标
t4 = ticks(l1) << anchor: 5 >>;  // 在坐标 5 处为零刻度
```

### 7. 刻度方向

```js
// 仅向上/向右
t1 = ticks(l1) <<
    majorTickEndings: [0, 1],
    tickEndings: [0, 1]
>>;

// 仅向下/向左
t2 = ticks(l1) <<
    majorTickEndings: [1, 0],
    tickEndings: [1, 0]
>>;

// 两侧（默认）
t3 = ticks(l1) <<
    majorTickEndings: [1, 1],
    tickEndings: [1, 1]
>>;
```

### 8. 自定义刻度标签

```js
// 自定义标签内容
t = ticks(l1) <<
    ticksDistance: 1,
    drawLabels: true,
    labels: ['A', 'B', 'C', 'D', 'E']
>>;
// 刻度位置会显示 A, B, C, D, E 而不是数字
```

### 9. 科学计数法美化

```js
// 美化大数字显示
t = ticks(l1) <<
    ticksDistance: 1000000,
    drawLabels: true,
    beautifulScientificTickLabels: true
>>;
// 5.00e+6 会显示为 5•10⁶
```

### 10. 滑块刻度

```js
// 滑块自带刻度
s = slider([1, 4], [4, 4], [0, 1, 10]) <<
    withTicks: true,
    ticks: <<
        minorTicks: 4,
        drawLabels: true
    >>
>>;
```

### 11. 坐标轴刻度

```js
// 创建 x 轴
xAxis = axis([-5, 0], [5, 0]) <<
    ticks: <<
        ticksDistance: 1,
        majorHeight: 10,
        minorTicks: 4,
        drawLabels: true,
        label: <<
            fontSize: 12,
            offset: [0, 10]
        >>
    >>
>>;

// 创建 y 轴
yAxis = axis([0, -5], [0, 5]) <<
    ticks: <<
        ticksDistance: 1,
        majorHeight: 10,
        drawLabels: true
    >>
>>;
```

### 12. 极坐标刻度

```js
// 极坐标刻度
t = ticks(curve) <<
    type: 'polar',
    ticksDistance: PI/4,  // 45 度
    drawLabels: true,
    label: <<
        toFraction: true,
        useMathjax: true
    >>
>>;
```

## 注意事项

1. **刻度距离**：`ticksDistance` 使用用户坐标，不是像素
2. **刻度高度**：`majorHeight` 和 `minorHeight` 使用像素，负数表示全高
3. **自动间距**：`insertTicks: true` 会根据画布大小自动计算合适的刻度间距
4. **标签格式化**：可以使用 `toFraction`, `useMathJax` 等属性美化标签显示
5. **最大刻度数**：当 `insertTicks: false` 时，最大刻度数限制为 2048

## 相关元素

- [Axis](./Axis.md) - 坐标轴（包含刻度）
- [Slider](./Slider.md) - 滑块（包含刻度）
- [Line](./Line.md) - 直线
- [Grid](./Grid.md) - 网格
