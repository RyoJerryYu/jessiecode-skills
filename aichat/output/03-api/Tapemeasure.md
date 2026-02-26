# Tapemeasure 卷尺

## 描述

卷尺用于测量点之间的距离。

卷尺的两个定义点（构成一条线段）默认不继承线段的 "visible" 属性。否则，当两个点重合且线段被隐藏时，卷尺将无法访问。

*定义于：* [measure.js](./src/src_element_measure.js.md)。
扩展自 [Segment](./Segment.md)。

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
   ➜ **[JXG.Line](./JXG.Line.md)**
      ➜ **[Segment](./Segment.md)**
            ➜ **Tapemeasure**

## JessieCode 语法

```js
// 基本语法 - 创建卷尺
tape = tapemeasure([x1, y1], [x2, y2]);

// 带属性创建
tape = tapemeasure([x1, y1], [x2, y2]) <<
    withLabel: true,
    name: 'dist',
    digits: 2
>>;

// 使用点创建卷尺
tape = tapemeasure(P1, P2);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| point1 | Point/Array | 第一个端点（坐标数组或点元素） |
| point2 | Point/Array | 第二个端点（坐标数组或点元素） |

## 属性

卷尺继承自 Segment，因此拥有 Segment 的所有属性。以下是卷尺特有的属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `digits` | Number | 2 | 卷尺测量值显示的小数位数 |
| `precision` | Number | 2 | 卷尺测量值显示的小数位数（已被 digits 替代） |
| `withLabel` | Boolean | true | 是否显示卷尺标签 |
| `withTicks` | Boolean | true | 是否显示卷尺刻度 |
| `rotate` | Number | 0 | 标签文本的旋转角度（度数） |
| `label` | Object | - | 卷尺标签的子属性 |
| `point1` | Object | - | 第一个辅助点的属性 |
| `point2` | Object | - | 第二个辅助点的属性 |
| `ticks` | Object | - | 刻度的子属性 |

### 子元素属性详解

#### point1 / point2

定义卷尺位置的两个辅助点的属性。这两个点默认不继承可见性，以便在两点重合时仍能操作卷尺。

```js
tape = tapemeasure([1, 2], [4, 2]) <<
    point1: <<
        visible: false,
        fixed: true
    >>,
    point2: <<
        visible: false
    >>
>>;
```

#### ticks

控制卷尺刻度的显示属性：

```js
tape = tapemeasure([1, 2], [4, 2]) <<
    withTicks: true,
    ticks: <<
        strokeColor: 'black',
        strokeWidth: 1,
        tickHeight: 5
    >>
>>;
```

#### label

控制卷尺标签的显示属性：

```js
tape = tapemeasure([1, 2], [4, 2]) <<
    withLabel: true,
    label: <<
        strokeColor: 'red',
        fontSize: 14,
        offset: [10, -10]
    >>
>>;
```

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `Value()` | 无 | 返回卷尺的长度 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `L(element)` | 获取线段/卷尺长度 | `L(tape)` |
| `dist(P, Q)` | 计算两点距离 | `dist(A, B)` |

## 示例

### 1. 创建基本卷尺

```js
// 使用坐标创建卷尺
tape = tapemeasure([1, 2], [4, 2]);

// 使用点创建卷尺
p1 = point(0, 0);
p2 = point(3, 4);
tape2 = tapemeasure(p1, p2);

// 卷尺会自动显示长度值
```

### 2. 设置卷尺样式

```js
// 带标签的卷尺
tape = tapemeasure([1, 2], [4, 2]) <<
    withLabel: true,
    name: 'dist',
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 隐藏刻度的卷尺
tape2 = tapemeasure([0, 0], [3, 3]) <<
    withTicks: false,
    strokeColor: 'red'
>>;
```

### 3. 设置小数位数

```js
// 精确到 2 位小数（默认）
tape1 = tapemeasure([1, 2], [4, 2]) <<
    digits: 2
>>;

// 精确到 3 位小数
tape2 = tapemeasure([0, 0], [3, 4]) <<
    digits: 3
>>;

// 不显示小数
tape3 = tapemeasure([1, 1], [4, 5]) <<
    digits: 0
>>;
```

### 4. 自定义标签

```js
// 自定义卷尺名称
tape = tapemeasure([1, 2], [4, 2]) <<
    withLabel: true,
    name: 'AB'
>>;

// 带单位的标签（需要结合 text 元素）
tape2 = tapemeasure([0, 0], [3, 4]) <<
    withLabel: false
>>;
label = text(2, 3, "距离：" + L(tape2) + " cm");
```

### 5. 旋转标签

```js
// 旋转标签文本 45 度
tape = tapemeasure([1, 2], [4, 5]) <<
    rotate: 45,
    withLabel: true
>>;

// 旋转标签文本 -30 度
tape2 = tapemeasure([0, 0], [3, 2]) <<
    rotate: -30
>>;
```

### 6. 动态卷尺

```js
// 创建可拖动的点
A = point(1, 1);
B = point(4, 3);

// 卷尺连接两个点
tape = tapemeasure(A, B) <<
    withLabel: true,
    digits: 2
>>;

// 拖动 A 或 B 点时，卷尺长度会实时更新
```

### 7. 卷尺与测量值

```js
// 创建卷尺
tape = tapemeasure([1, 2], [4, 2]) <<
    name: 'd1',
    withLabel: true
>>;

// 使用测量元素显示卷尺长度
m = measurement(2, 3, ['L', tape], <<
    prefix: '长度：',
    baseUnit: 'cm'
>>);
```

### 8. 多个卷尺比较

```js
// 创建多个卷尺进行测量比较
tape1 = tapemeasure([0, 0], [3, 0]) <<
    name: 'd1',
    strokeColor: 'red'
>>;

tape2 = tapemeasure([0, 1], [3, 1]) <<
    name: 'd2',
    strokeColor: 'blue'
>>;

tape3 = tapemeasure([0, 2], [3, 2]) <<
    name: 'd3',
    strokeColor: 'green'
>>;

// 显示总长度
total = measurement(4, 1,
    ['+', ['L', tape1], ['L', tape2], ['L', tape3]], <<
    prefix: '总长度：'
>>);
```

### 9. 卷尺辅助点属性

```js
// 自定义辅助点样式
tape = tapemeasure([1, 2], [4, 2]) <<
    point1: <<
        visible: true,
        fixed: false,
        strokeColor: 'red',
        size: 5
    >>,
    point2: <<
        visible: true,
        fixed: false,
        strokeColor: 'blue',
        size: 5
    >>
>>;
```

### 10. 卷尺刻度属性

```js
// 自定义刻度样式
tape = tapemeasure([1, 2], [5, 2]) <<
    withTicks: true,
    ticks: <<
        strokeColor: 'black',
        strokeWidth: 2,
        tickHeight: 8,
        minorTicks: 4
    >>
>>;
```

## 注意事项

1. **继承 Segment**：卷尺是线段的子类，拥有线段的所有属性和方法
2. **可见性独立**：卷尺的两个定义点默认不继承可见性，确保在两点重合时仍能操作
3. **自动测量**：卷尺会自动显示两端点之间的距离
4. **digits 与 precision**：`precision` 属性已被 `digits` 替代，建议使用 `digits`
5. **标签显示**：默认显示标签，可通过 `withLabel: false` 隐藏
6. **刻度显示**：默认显示刻度，可通过 `withTicks: false` 隐藏
7. **动态更新**：当卷尺端点移动时，测量值会自动更新

## 相关元素

- [Segment](./Segment.md) - 线段（父类）
- [Line](./Line.md) - 直线
- [Measurement](./Measurement.md) - 测量（用于显示测量值）
- [Text](./Text.md) - 文本（用于添加自定义标签）
- [Point](./Point.md) - 点（卷尺的端点）
