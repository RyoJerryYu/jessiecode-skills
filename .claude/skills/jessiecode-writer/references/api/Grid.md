# Grid 网格

<!-- USAGE_FREQUENCY: advanced -->

## 描述

网格是由垂直和水平线或其他几何对象组成的网状结构，用于支持用户放置元素或提高位置确定的准确性。

**继承关系**

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
   ↳ **[JXG.Curve](./JXG.Curve.md)**
      ↳ **Grid**

## JessieCode 语法

```js
// 创建标准网格
g = create('grid', [], {});

// 创建带属性的网格
g = create('grid', [], <<
    major: <<
        face: 'plus',
        size: 7,
        strokeColor: 'green',
        strokeOpacity: 1
    >>,
    minor: <<
        size: 4
    >>,
    minorElements: 3
>>);

// 使用坐标轴作为父元素的网格
g = create('grid', [axis1, axis2], {});
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| axis1 | Axis | 可选的第一个父坐标轴 |
| axis2 | Axis | 可选的第二个父坐标轴 |

**注意**：此元素没有直接构造函数。必须使用 `board.create('grid', ...)` 或 JessieCode 的 `create()` 函数来创建实例。

## 属性

### 基本属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `majorStep` | String/Number/Array | 'auto' | 主网格元素的间距 |
| `minorElements` | String/Number/Array | 0 | 主网格之间的次网格元素数量 |
| `forceSquare` | Boolean/String | false | 是否强制正方形网格 |
| `includeBoundaries` | Boolean | false | 是否在边界上显示网格元素 |
| `margin` | Number | 0 | 网格元素在画布边缘的边距 |

### major 对象（主网格）

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `size` | Number/String/Array | 5 | 主网格元素的大小 |
| `face` | String | 'line' | 主网格元素的外观样式 |
| `margin` | Number | 0 | 主网格的边距 |
| `drawZero` | Boolean/Object | true | 是否显示零位置的网格元素 |
| `polygonVertices` | Number | 6 | 正多边形样式的顶点数 |

### minor 对象（次网格）

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `size` | Number/String/Array | 3 | 次网格元素的大小 |
| `face` | String | 'point' | 次网格元素的外观样式 |
| `margin` | Number | 0 | 次网格的边距 |
| `drawZero` | Boolean/Object | true | 是否显示零位置的网格元素 |
| `polygonVertices` | Number | 6 | 正多边形样式的顶点数 |

### majorStep 详解

| 值类型 | 说明 |
|--------|------|
| `'auto'` | 间距等于对应坐标轴主刻度的间距 |
| `Number` | 解释为用户坐标中的距离 |
| `String` (如 '10') | 解释为用户坐标中的距离 |
| `String` (如 '10px') | 解释为屏幕像素中的距离 |
| `String` (如 '50%' 或 '0.5fr') | 解释为相对于画板宽度/高度的比例 |
| `Array` [x, y] | 分别设置 x 和 y 方向的间距 |

### minorElements 详解

| 值类型 | 说明 |
|--------|------|
| `'auto'` | 数量等于对应坐标轴次刻度的数量 |
| `Number` | 解释为数量 |
| `String` (如 '10') | 解释为数量 |
| `Array` [x, y] | 分别设置 x 和 y 方向的数量 |

### size 详解

| 值类型 | 说明 |
|--------|------|
| `Number` | 解释为像素大小 |
| `String` (如 '10') | 解释为像素大小 |
| `String` (如 '95%') | 解释为每个元素使用空间的比例 |
| `Array` [x, y] | 分别设置 x 和 y 方向的大小 |

**注意**：`size` 属性对 `face: 'line'` 无效，将使用 `strokeWidth` 的值。

### face 样式选项

| 输入值 | 输出样式 | 是否可用 fillColor 填充 |
|--------|----------|------------------------|
| `point`, `.` | . | 否 |
| `line` | − | 否 |
| `cross`, `x` | x | 否 |
| `circle`, `o` | o | 是 |
| `square`, `[]` | [] | 是 |
| `plus`, `+` | + | 否 |
| `minus`, `-` | - | 否 |
| `divide`, `\|` | \| | 否 |
| `diamond`, `<>` | <> | 是 |
| `diamond2`, `<<>>` | <> (更大) | 是 |
| `triangleup`, `^`, `a`, `A` | ^ | 否 |
| `triangledown`, `v` | v | 否 |
| `triangleleft`, `<` | < | 否 |
| `triangleright`, `>` | > | 否 |
| `regularPolygon`, `regpol` | ⬡ | 是 |

### drawZero 详解

此属性确定是否显示位于 x=0、y=0 和（仅主网格）原点 (0, 0) 的网格元素。

| 值 | 说明 |
|----|------|
| `false` | 隐藏所有这些元素 |
| `true` | 显示所有这些元素 |
| `Object` | 可以分别设置：`{x: true/false, y: true/false, origin: true/false}` |

### forceSquare 详解

用于打印正方形网格，使 x 和 y 方向的主网格元素间距相同。

| 值 | 说明 |
|----|------|
| `false` | 不强制正方形网格（默认） |
| `true` 或 `'min'` | 将两个方向的间距设置为较小的值 |
| `'max'` | 将两个方向的间距设置为较大的值 |

### includeBoundaries 详解

| 值 | 说明 |
|----|------|
| `false` | 不在边界框的边界上显示网格元素 |
| `true` | 在边界框的边界上显示网格元素（包括半元素） |

## 示例

### 1. 创建基本网格

```js
// 标准网格
g = create('grid', [], {});
```

### 2. 带属性的网格

```js
// 更美观的网格
g = create('grid', [], <<
    major: <<
        face: 'plus',
        size: 7,
        strokeColor: 'green',
        strokeOpacity: 1
    >>,
    minor: <<
        size: 4
    >>,
    minorElements: 3
>>);
```

### 3. 使用正多边形的网格

```js
// 使用正多边形的网格
grid = create('grid', [], <<
    major: <<
        face: 'regularPolygon',
        size: 8,
        strokeColor: 'blue',
        fillColor: 'orange',
        strokeOpacity: 1
    >>,
    minor: <<
        face: 'diamond',
        size: 4,
        strokeColor: 'green',
        fillColor: 'grey'
    >>,
    minorElements: 1,
    includeBoundaries: false
>>);
```

### 4. 带父坐标轴的网格

```js
// 创建第一个坐标轴
axis1 = create('axis', [[-1, -2.5], [1, -2.5]], <<
    ticks: <<
        strokeColor: 'green',
        strokeWidth: 2,
        minorticks: 2,
        majorHeight: 10,
        drawZero: true
    >>
>>);

// 创建第二个坐标轴
axis2 = create('axis', [[3, 0], [3, 2]], <<
    ticks: <<
        strokeColor: 'red',
        strokeWidth: 2,
        minorticks: 3,
        majorHeight: 10,
        drawZero: true
    >>
>>);

// 使用坐标轴创建网格
grid = create('grid', [axis1, axis2], <<
    major: <<
        face: 'line'
    >>,
    minor: <<
        face: 'point',
        size: 3
    >>,
    minorElements: 'auto',
    includeBoundaries: false
>>);
```

### 5. 设置网格间距

```js
// 固定间距的网格
g1 = create('grid', [], <<
    majorStep: 2,
    minorElements: 4
>>);

// 使用像素间距
g2 = create('grid', [], <<
    majorStep: '20px'
>>);

// 分别设置 x 和 y 方向的间距
g3 = create('grid', [], <<
    majorStep: [1, 2]
>>);
```

### 6. 不同样式的网格

```js
// 圆形网格
g1 = create('grid', [], <<
    major: <<
        face: 'circle',
        strokeColor: 'red',
        fillColor: 'pink'
    >>
>>);

// 方形网格
g2 = create('grid', [], <<
    major: <<
        face: 'square',
        strokeColor: 'blue',
        fillColor: 'lightblue'
    >>
>>);

// 菱形网格
g3 = create('grid', [], <<
    major: <<
        face: 'diamond',
        strokeColor: 'green',
        fillColor: 'lightgreen'
    >>
>>);
```

### 7. 不显示零位置的网格

```js
// 与坐标轴配合使用时隐藏零位置
g = create('grid', [], <<
    major: <<
        drawZero: false
    >>,
    minor: <<
        drawZero: false
    >>
>>);

// 或者分别控制
g2 = create('grid', [], <<
    major: <<
        drawZero: <<
            x: false,
            y: false,
            origin: false
        >>
    >>
>>);
```

### 8. 正方形网格

```js
// 强制正方形网格（使用较小的间距值）
g1 = create('grid', [], <<
    forceSquare: true
>>);

// 使用较大的间距值
g2 = create('grid', [], <<
    forceSquare: 'max'
>>);
```

### 9. 显示边界上的网格元素

```js
// 在边界上显示网格元素
g = create('grid', [], <<
    includeBoundaries: true
>>);
```

### 10. 设置网格元素大小

```js
// 固定像素大小
g1 = create('grid', [], <<
    major: <<
        size: 8
    >>,
    minor: <<
        size: 4
    >>
>>);

// 使用百分比大小（元素间距的百分比）
g2 = create('grid', [], <<
    major: <<
        size: '90%'
    >>
>>);

// 分别设置 x 和 y 方向的大小
g3 = create('grid', [], <<
    major: <<
        size: [5, 10]
    >>
>>);
```

## 注意事项

1. **创建方式**：网格元素没有直接构造函数，必须使用 `create('grid', ...)` 创建
2. **坐标轴依赖**：当 `majorStep` 或 `minorElements` 设置为 'auto' 时，网格会使用对应坐标轴的刻度设置
3. **分别设置**：`major` 和 `minor` 对象可以分别设置主网格和次网格的属性
4. **零位置显示**：与坐标轴配合使用时，通常设置 `drawZero: false` 以避免重复显示
5. **正方形网格**：`forceSquare` 属性可以确保 x 和 y 方向的间距相同
6. **边界元素**：`includeBoundaries` 控制是否在画布边界显示网格元素

## 相关元素

- [Axis](./Axis.md) - 坐标轴
- [Ticks](./Ticks.md) - 刻度
- [Point](./Point.md) - 点
- [Line](./Line.md) - 直线
