# Smartlabel 智能标签

<!-- USAGE_FREQUENCY: advanced -->

## 描述

智能标签是用于显示 JSXGraph 元素测量值的自定义文本元素。例如：线段的长度、圆或多边形的周长或面积（包括多边形链）、直线的斜率、角度的值以及点的坐标。

如果还提供了文本或函数，且内容不是空字符串，则该文本将覆盖测量值。

智能标签使用 jsxgraph.css 中定义的自定义 CSS 布局。因此，必须包含 jsxgraph.css 文件，或者必须用其他类替换 CSS 类。

智能标签的默认属性根据测量元素的类型在不同子对象中定义。这与通常的 JSXGraph 属性用法有所不同。

## JessieCode 语法

```js
// 基本语法 - 显示点的坐标
sl = smartlabel(point) <<
    digits: 1,
    unit: 'm',
    dir: 'col'
>>;

// 显示线段长度
sl = smartlabel(line) <<
    measure: 'length',
    prefix: 'L = ',
    unit: 'm'
>>;

// 显示直线斜率
sl = smartlabel(line) <<
    measure: 'slope',
    prefix: 'Δ = '
>>;

// 显示圆的周长/面积/半径
sl = smartlabel(circle) <<
    measure: 'perimeter',
    prefix: 'U = ',
    unit: 'm'
>>;

sl = smartlabel(circle) <<
    measure: 'area',
    prefix: 'A = ',
    unit: 'm'
>>;

sl = smartlabel(circle) <<
    measure: 'radius',
    prefix: 'R = '
>>;

// 显示多边形面积/周长
sl = smartlabel(polygon) <<
    measure: 'area',
    prefix: 'A = ',
    unit: 'm'
>>;

// 显示角度值
sl = smartlabel(angle) <<
    digits: 1,
    prefix: 'β = ',
    unit: '°'
>>;

// 使用自定义文本覆盖测量值
sl = smartlabel(polygon, function() { return 'X: ' + polygon.vertices[0].X().toFixed(1); }) <<
    measure: 'perimeter'
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| Parent | GeometryElement | 父对象：点、直线、圆、多边形、角度 |
| Txt | String/Function | 可选文本。如果内容不是空字符串，测量值将被此文本覆盖 |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `cssClass` | String | 根据元素类型 | 智能标签的 CSS 类 |
| `dir` | String | 'row' | 点坐标显示方式：'row'（行向量）或 'column'（列向量） |
| `highlightCssClass` | String | 根据元素类型 | 高亮时智能标签的 CSS 类 |
| `measure` | String | 根据元素类型 | 测量类型 |
| `prefix` | String | '' | 智能标签前缀文本 |
| `suffix` | String | '' | 智能标签后缀文本 |
| `unit` | String | '' | 测量单位，附加到输出文本 |
| `digits` | Number | 2 | 小数位数 |
| `useMathJax` | Boolean | false | 使用 MathJax 渲染 |

### CSS 类 (cssClass)

可用的 CSS 类：

| 类名 | 描述 |
|------|------|
| `smart-label-solid` | 实心样式 |
| `smart-label-outline` | 轮廓样式 |
| `smart-label-pure` | 纯色样式 |

默认情况下，会根据元素类型添加额外的特定类：

| 元素类型 | CSS 类 |
|----------|--------|
| 圆 | `smart-label-circle` |
| 点 | `smart-label-point` |
| 直线 | `smart-label-line` |
| 多边形 | `smart-label-polygon` |
| 角度 | `smart-label-angle` |

### 测量类型 (measure)

| 元素类型 | 可用值 | 默认值 |
|----------|--------|--------|
| 角度 | `deg`（度）, `rad`（弧度） | `deg` |
| 圆 | `area`（面积）, `perimeter`（周长）, `radius`（半径） | `radius` |
| 直线 | `length`（长度）, `slope`（斜率） | `length` |
| 多边形 | `area`（面积）, `perimeter`（周长） | `area` |

根据测量类型的不同，标签在对象上的位置也会不同。

### 方向 (dir)

| 值 | 描述 | 示例 |
|------|------|------|
| `row` | 行向量显示 | (1.5, 2.5) |
| `column` | 列向量显示 | (1.5<br>2.5) |

## 示例

### 1. 显示点的坐标

```js
// 创建点
p1 = point(3, 4) << showInfobox: false, withLabel: false >>;

// 显示点的坐标（列向量格式）
sl = smartlabel(p1) <<
    digits: 1,
    unit: 'm',
    dir: 'col',
    useMathJax: false
>>;
```

### 2. 显示直线的长度和斜率

```js
// 创建直线
s1 = line([-7, 2], [6, -6]) <<
    point1: << visible: true >>,
    point2: << visible: true >>
>>;

// 显示长度
sl1 = smartlabel(s1) <<
    unit: 'm',
    measure: 'length',
    prefix: 'L = ',
    useMathJax: false
>>;

// 显示斜率
sl2 = smartlabel(s1) <<
    unit: 'm',
    measure: 'slope',
    prefix: 'Δ = ',
    useMathJax: false
>>;
```

### 3. 显示圆的属性

```js
// 创建圆
c1 = circle([0, 1], [4, 1]) << point2: << visible: true >> >>;

// 显示周长
sl1 = smartlabel(c1) <<
    unit: 'm',
    measure: 'perimeter',
    prefix: 'U = ',
    useMathJax: false
>>;

// 显示面积
sl2 = smartlabel(c1) <<
    unit: 'm',
    measure: 'area',
    prefix: 'A = ',
    useMathJax: false
>>;

// 显示半径
sl3 = smartlabel(c1) <<
    unit: 'm',
    measure: 'radius',
    prefix: 'R = ',
    useMathJax: false
>>;
```

### 4. 显示多边形的属性

```js
// 创建多边形
p2 = polygon([-6, -5], [7, -7], [-4, 3]);

// 显示面积（纯色样式）
sl1 = smartlabel(p2) <<
    unit: 'm',
    measure: 'area',
    prefix: 'A = ',
    cssClass: 'smart-label-pure smart-label-polygon',
    highlightCssClass: 'smart-label-pure smart-label-polygon',
    useMathJax: false
>>;

// 显示周长（轮廓样式，使用自定义文本）
sl2 = smartlabel(p2, function() {
    return 'X: ' + p2.vertices[0].X().toFixed(1);
}) <<
    measure: 'perimeter',
    cssClass: 'smart-label-outline smart-label-polygon',
    highlightCssClass: 'smart-label-outline smart-label-polygon',
    useMathJax: false
>>;
```

### 5. 显示角度值

```js
// 创建角度
a1 = angle([1, -1], [1, 2], [1, 5]) <<
    name: 'β',
    withLabel: false
>>;

// 显示角度值
sl = smartlabel(a1) <<
    digits: 1,
    prefix: a1.name + '=',
    unit: '°',
    useMathJax: false
>>;
```

### 6. 自定义样式组合

```js
// 创建线段和智能标签
A = point(0, 0) << withLabel: true, name: 'A' >>;
B = point(3, 4) << withLabel: true, name: 'B' >>;
seg = segment(A, B);

// 显示距离，使用不同样式
distLabel = smartlabel(seg) <<
    measure: 'length',
    prefix: 'AB = ',
    unit: 'm',
    digits: 2,
    cssClass: 'smart-label-solid smart-label-line',
    fontSize: 14
>>;
```

## 注意事项

1. **CSS 依赖**：智能标签依赖于 jsxgraph.css 中定义的 CSS 类，必须包含该文件
2. **测量类型**：不同元素类型支持不同的测量类型，需根据元素选择合适的 `measure` 值
3. **自定义文本**：可以通过提供第二个参数（文本或函数）来覆盖默认测量值
4. **单位处理**：对于面积，单位会自动平方（如 'm' 变为 'm²'）
5. **位置自动调整**：标签根据测量类型自动定位在元素的不同位置
6. **非直接构造函数**：智能标签没有直接的构造函数，必须通过 `board.create('smartlabel', ...)` 创建

## 相关元素

- [Text](./Text.md) - 文本元素
- [Label](./Label.md) - 标签（元素的子标签）
- [Point](./Point.md) - 点
- [Segment](./Segment.md) - 线段
- [Circle](./Circle.md) - 圆
- [Polygon](./Polygon.md) - 多边形
- [Angle](./Angle.md) - 角度
