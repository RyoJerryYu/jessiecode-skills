# Label 标签

<!-- USAGE_FREQUENCY: advanced -->

## 描述

标签是绑定到其他元素（如点、线和曲线）的文本对象。标签由 JSXGraph 内部管理，没有构造函数 `board.create('label', ...)`。

*定义于：* [text.js](./src/src_base_text.js.md)。

继承自 [JXG.Text](./JXG.Text.md)。

## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md), JXG.GeometryElement**
   ↳ **[JXG.Text](./JXG.Text.md)**
         ↳ **Label**

## JessieCode 语法

```js
// 标签通常自动创建，当设置点的 withLabel: true 时
A = point(1, 2) <<
    withLabel: true,
    name: 'A'
>>;

// 直线标签
l = line(A, B) <<
    withLabel: true,
    name: 'l'
>>;

// 自定义标签位置
A = point(1, 2) <<
    withLabel: true,
    label: <<
        offset: [20, -10],
        position: 'lrt'
    >>
>>;

// 沿路径的标签（线、圆、曲线）
l = line(A, B) <<
    withLabel: true,
    label: <<
        position: '50% left'
    >>
>>;
```

## 参数

标签通常作为其他元素的属性创建，主要参数如下：

| 参数 | 类型 | 描述 |
|------|------|------|
| `withLabel` | Boolean | 是否显示标签 |
| `name` | String | 标签文本内容 |
| `label` | Object | 标签属性配置对象 |

## 属性

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `autoPosition` | Boolean | false | 自动定位标签文本 |
| `autoPositionMaxDistance` | Number | 28 | 自动定位算法的最大距离（像素） |
| `autoPositionMinDistance` | Number | 12 | 自动定位算法的最小距离（像素） |
| `autoPositionWhitelist` | Array | [] | 自动定位时应忽略的对象 ID 列表 |
| `distance` | Number | 1.5 | 标签与路径元素（线、圆、曲线）的距离 |
| `offset` | Array | [10, 10] | 标签相对于锚点的偏移量 |
| `position` | String | 'urt' | 标签位置 |

### autoPosition (Boolean)

自动定位标签文本。首次调用时，定位算法从 `offset` 定义的位置开始。
算法尝试找到一个与其他元素重叠最少的位置，同时保持与锚点元素的距离。

**默认值：** `false`

**另见：**
- [Label#offset](#offset)
- GeometryElement#ignoreForLabelAutoposition
- [Label#autoPositionMinDistance](#autoPositionMinDistance)
- [Label#autoPositionMaxDistance](#autoPositionMaxDistance)
- [Label#autoPositionWhitelist](#autoPositionWhitelist)

### autoPositionMaxDistance (Number)

自动定位算法尝试将标签放置在锚点周围无冲突的位置。
算法会在锚点周围测试 12 个位置，最大距离由此属性定义（以像素为单位）。

**默认值：** `28`

**另见：**
- [Label#autoPosition](#autoPosition)
- [Label#autoPositionMinDistance](#autoPositionMinDistance)
- [Label#autoPositionWhitelist](#autoPositionWhitelist)

### autoPositionMinDistance (Number)

自动定位算法尝试将标签放置在锚点周围无冲突的位置。
算法会在锚点周围测试 12 个位置，起始距离由此属性定义（以像素为单位）。

**默认值：** `12`

**另见：**
- [Label#autoPosition](#autoPosition)
- [Label#autoPositionMaxDistance](#autoPositionMaxDistance)
- [Label#autoPositionWhitelist](#autoPositionWhitelist)

### autoPositionWhitelist (Array)

在设置标签文本自动位置时应忽略的对象 ID 列表。

**默认值：** `[]`

**另见：**
- [Label#autoPosition](#autoPosition)
- [Label#autoPositionMinDistance](#autoPositionMinDistance)
- [Label#autoPositionMaxDistance](#autoPositionMaxDistance)

### distance (Number)

标签与路径元素（如线、圆、曲线）的距离。
实际距离是此值乘以标签文本边界框大小的 0.5 倍。
也就是说，值为 1 时标签将接触路径元素。

**默认值：** `1.5`

**另见：**
- [Label#position](#position)

### offset (Array)

标签相对于标签锚点的偏移量。
标签锚点由 [Label#position](#position) 确定。

**默认值：** `[10, 10]`

**另见：**
- [Label#position](#position)

### position (String)

点的标签通过设置 `Point#anchorX`、`Point#anchorY` 和 [Label#offset](#offset) 来定位。

对于线、圆和曲线元素（及其派生对象），有两种定位标签的方式：

**第一种方式（旧方法）：** 使用 [MetaPost](https://www.tug.org/metapost.html) 系统

标签锚点位置的有效字符串值：
- `'first'` - 仅用于直线，第一个点位置
- `'last'` - 仅用于直线，最后一个点位置
- `'lft'` - 左侧
- `'rt'` - 右侧
- `'top'` - 顶部
- `'bot'` - 底部
- `'ulft'` - 左上
- `'urt'` - 右上（默认值）
- `'llft'` - 左下
- `'lrt'` - 右下

**第二种方式（推荐，v1.9.0+）：** 使用 `'len side'` 格式

标签可以沿元素路径精确定位。格式为 `position: 'len side'`：

- `len` 是以下形式的表达式：
  - `xfr` - 表示分数，x 应该是 0 到 1 之间的数字
  - `x%` - 百分比，x 应该是 0 到 100 之间的数字
  - `x` - 数字：仅适用于直线元素和圆
    - 对于直线：标签定位在距起点 x 用户单位处
    - 对于圆：数字解释为角度，例如 45 度
    - 对于其他元素：使用 0
  - `xpx` - 像素值：仅适用于直线元素
    - 标签定位在距起点 x 像素处
    - 对于非直线元素：使用 0%

- `side` 是 `'left'` 或 `'right'`
  - 标签定位在从第一个点到最后一个点移动时路径的左侧或右侧
  - 对于圆：`'left'` 表示圆内，`'right'` 表示圆外
  - 标签与路径的距离可通过 [Label#distance](#distance) 控制

对于第二种方式，建议使用 `anchorX: 'middle'` 和 `anchorY: 'middle'`。

**默认值：** `'urt'`

**另见：**
- [Label#distance](#distance)
- [Label#offset](#offset)

## 示例

### 1. 基本标签

```js
// 带标签的点
A = point(1, 2) <<
    withLabel: true,
    name: 'A'
>>;

// 带标签的直线
B = point(3, 4);
l = line(A, B) <<
    withLabel: true,
    name: 'l'
>>;
```

### 2. 自定义标签偏移

```js
// 修改标签偏移量
A = point(1, 2) <<
    withLabel: true,
    name: 'A',
    label: <<
        offset: [30, -20]
    >>
>>;

// 更大的偏移
B = point(3, 1) <<
    withLabel: true,
    name: 'B',
    label: <<
        offset: [50, 50]
    >>
>>;
```

### 3. 标签位置（点的标签）

```js
// 使用 MetaPost 风格的位置
A = point(1, 2) <<
    withLabel: true,
    name: 'A',
    label: <<
        position: 'urt'  // 右上
    >>
>>;

B = point(3, 2) <<
    withLabel: true,
    name: 'B',
    label: <<
        position: 'llft'  // 左下
    >>
>>;

C = point(5, 2) <<
    withLabel: true,
    name: 'C',
    label: <<
        position: 'top'  // 顶部
    >>
>>;

D = point(7, 2) <<
    withLabel: true,
    name: 'D',
    label: <<
        position: 'bot'  // 底部
    >>
>>;
```

### 4. 直线标签位置

```js
A = point(1, 1);
B = point(5, 3);

// 在直线起点
l1 = line(A, B) <<
    withLabel: true,
    name: 'l1',
    label: <<
        position: 'first'
    >>
>>;

// 在直线终点
l2 = line(A, C) <<
    withLabel: true,
    name: 'l2',
    label: <<
        position: 'last'
    >>
>>;
```

### 5. 沿路径的标签（推荐方式）

```js
A = point(1, 1);
B = point(5, 3);
l = line(A, B);

// 在直线的 50% 位置，左侧
lbl1 = text(l, '中点') <<
    position: '50% left',
    anchorX: 'middle',
    anchorY: 'middle'
>>;

// 在直线的 25% 位置，右侧
lbl2 = text(l, '25%') <<
    position: '25% right',
    anchorX: 'middle',
    anchorY: 'middle'
>>;

// 在直线的 75% 位置，右侧
lbl3 = text(l, '75%') <<
    position: '75% right',
    anchorX: 'middle',
    anchorY: 'middle'
>>;
```

### 6. 圆的标签

```js
// 创建圆
O = point(0, 0);
A = point(3, 0);
c = circle(O, A);

// 圆内标签（left = 内部）
lbl1 = text(c, '圆内') <<
    position: '45deg left',
    anchorX: 'middle',
    anchorY: 'middle'
>>;

// 圆外标签（right = 外部）
lbl2 = text(c, '圆外') <<
    position: '45deg right',
    anchorX: 'middle',
    anchorY: 'middle',
    distance: 2
>>;
```

### 7. 自动定位

```js
// 启用自动定位
A = point(1, 2) <<
    withLabel: true,
    name: 'A',
    label: <<
        autoPosition: true
    >>
>>;

// 自定义自动定位距离
B = point(3, 2) <<
    withLabel: true,
    name: 'B',
    label: <<
        autoPosition: true,
        autoPositionMinDistance: 15,
        autoPositionMaxDistance: 35
    >>
>>;

// 忽略某些元素的自动定位
C = point(5, 2) <<
    withLabel: true,
    name: 'C',
    label: <<
        autoPosition: true,
        autoPositionWhitelist: ['A', 'B']
    >>
>>;
```

### 8. 曲线标签

```js
// 创建曲线
curve1 = curve(function(t) { return t; },
               function(t) { return sin(t); },
               0, 2*PI);

// 在曲线的中点
lbl = text(curve1, '正弦曲线') <<
    position: '0.5fr left',
    anchorX: 'middle',
    anchorY: 'middle'
>>;
```

### 9. 使用分数和百分比

```js
A = point(0, 0);
B = point(8, 0);
l = line(A, B);

// 使用分数 (0.25 = 25%)
lbl1 = text(l, '1/4') <<
    position: '0.25fr right',
    anchorX: 'middle',
    anchorY: 'middle'
>>;

// 使用百分比
lbl2 = text(l, '50%') <<
    position: '50% right',
    anchorX: 'middle',
    anchorY: 'middle'
>>;

// 使用 3/4 分数
lbl3 = text(l, '3/4') <<
    position: '0.75fr right',
    anchorX: 'middle',
    anchorY: 'middle'
>>;
```

### 10. 使用像素距离

```js
A = point(0, 0);
B = point(10, 0);
l = line(A, B);

// 从起点 100 像素处
lbl = text(l, '100px') <<
    position: '100px right',
    anchorX: 'middle',
    anchorY: 'middle'
>>;
```

## 注意事项

1. **标签不能直接创建**：标签总是作为其他元素的属性自动创建，没有独立的构造函数
2. **两种定位方式**：推荐使用新的 `'len side'` 格式（v1.9.0+），更精确且灵活
3. **MetaPost 位置值**：`'urt'` (右上) 是默认位置，其他值包括 `'lft'`, `'rt'`, `'top'`, `'bot'` 等
4. **自动定位**：启用 `autoPosition: true` 可避免标签与其他元素重叠
5. **圆标签方向**：对于圆，`'left'` 表示圆内，`'right'` 表示圆外
6. **曲线标签**：如果曲线的定义域不连通，标签会定位在曲线首尾点连线附近
7. **推荐设置**：使用新定位方式时，建议设置 `anchorX: 'middle'` 和 `anchorY: 'middle'`

## 相关元素

- [Text](./Text.md) - 文本对象
- [Point](./Point.md) - 点（通常带标签）
- [Line](./Line.md) - 直线（可带标签）
- [Circle](./Circle.md) - 圆（可带标签）
- [Curve](./Curve.md) - 曲线（可带标签）
