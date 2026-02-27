# Measurement 测量

<!-- USAGE_FREQUENCY: advanced -->

## 描述

测量是用于显示几何元素的测量值以及测量值的算术运算。在内部，这是一个具有 Value 方法的文本元素。要显示的文本是前缀表达式求值的结果，参见 [JXG.PrefixParser](./JXG.PrefixParser.md)。

此元素的目的是显示几何对象的测量值，如圆的半径，以及由测量值组成的表达式。

*定义于：* [measure.js](./src/src_element_measure.js.md)，扩展自 [Text](./Text.md)。

## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md), JXG.GeometryElement**
   ↳ **[JXG.Text](./JXG.Text.md)**
      ↳ **[Text](./Text.md)**
            ↳ **Measurement**

## JessieCode 语法

```js
// 基本语法 - 显示几何元素的测量值
m = measurement(x, y, ['MeasureType', element], <<
    prefix: '值：',
    baseUnit: 'cm'
>>);

// 测量圆的面积
m = measurement(1, -2, ['Area', circle]);

// 测量线段长度
m = measurement(1, -4, ['L', segment]);

// 测量滑块值
m = measurement(-6, -6, ['V', slider]);

// 算术运算 - 多个测量值相加
m = measurement(2, -6,
    ['+', ['V', m1], ['V', m2], ['V', m3]]
);
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| x | Number/Point/Array | 显示位置的 x 坐标或参考点 |
| y | Number/Array | 显示位置的 y 坐标 |
| expression | Array | 前缀表达式，定义要测量的内容 |

### 表达式格式

表达式是一个前缀表达式数组，第一个元素是操作符，后续元素是操作数：

| 操作符 | 描述 | 示例 |
|--------|------|------|
| `Area` | 测量面积 | `['Area', circle]` |
| `Radius` | 测量半径 | `['Radius', circle]` |
| `L` | 测量长度 | `['L', segment]` |
| `V` | 获取值 | `['V', slider]` 或 `['V', measurement]` |
| `+` | 加法运算 | `['+', ['V', m1], ['V', m2]]` |
| `-` | 减法运算 | `['-', ['V', m1], ['V', m2]]` |
| `*` | 乘法运算 | `['*', ['V', m1], 2]` |
| `/` | 除法运算 | `['/', ['V', m1], 2]` |

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `baseUnit` | String | '' | 指定维度 1（如长度）的测量单位 |
| `dim` | Number/'coords'/'direction' | null | 测量数据的维度 |
| `formatCoords` | Function | - | 格式化坐标的函数 |
| `formatDirection` | Function | - | 格式化方向向量的函数 |
| `prefix` | String | '' | 显示在测量值和单位之前的字符串 |
| `showPrefix` | Boolean | true | 是否显示前缀 |
| `showSuffix` | Boolean | true | 是否显示后缀 |
| `suffix` | String | '' | 显示在测量值和单位之后的字符串 |
| `units` | Object | - | 为不同维度指定单位的对象 |

### 属性详解

#### baseUnit

指定维度 1（如长度）的测量单位。字符串会自动添加幂次。
如果要为每个维度使用不同的单位，请使用 `units` 属性。

```js
m = measurement(1, -2, ['Area', circle], <<
    baseUnit: 'cm'  // 面积将显示为 cm²
>>);
```

#### dim

测量数据的维度。此测量只能与合适维度的测量组合。
会覆盖 `Dimension()` 方法返回的维度。
通常使用默认值 `null` 来自动确定维度。
但是，如果测量坐标或方向向量，返回值通常是数组。
为了告诉测量使用 `formatCoords` 或 `formatDirection` 函数来正确显示数组，
需要在此处设置为 `'coords'` 或 `'direction'`。

```js
// 显示坐标
m = measurement(1, 1, ['X', point], <<
    dim: 'coords',
    formatCoords: function(coords) {
        return '(' + coords[0] + ', ' + coords[1] + ')';
    }
>>);

// 显示方向向量
m = measurement(1, 2, ['direction', line], <<
    dim: 'direction'
>>);
```

#### prefix / showPrefix

`prefix` 是显示在测量值和单位之前的字符串。
`showPrefix` 决定是否显示前缀。

```js
m = measurement(1, -2, ['Area', circle], <<
    prefix: '面积：',
    showPrefix: true
>>);  // 显示："面积：12.57 cm²"
```

#### suffix / showSuffix

`suffix` 是显示在测量值和单位之后的字符串。
`showSuffix` 决定是否显示后缀。

```js
m = measurement(1, -2, ['L', segment], <<
    suffix: '（长度）',
    showSuffix: true
>>);  // 显示："5.00 cm（长度）"
```

#### units

此属性需要一个对象，以维度数字作为键（整数或 "dimxx" 形式），
并为每个维度分配一个字符串。
如果某个维度没有指定，则使用 `baseUnit`。

```js
m = measurement(1, -2, ['Volume', box], <<
    units: <<
        dim1: 'm',
        dim2: 'm²',
        dim3: 'm³'
    >>
>>);
```

## 示例

### 1. 基本测量

```js
// 创建几何元素
p1 = point(1, 1);
p2 = point(1, 3);
circle = circle(p1, p2);

// 测量圆的面积
m1 = measurement(1, -2, ['Area', circle], <<
    visible: true,
    prefix: '面积：',
    baseUnit: 'cm'
>>);

// 测量圆的半径
m2 = measurement(1, -4, ['Radius', circle], <<
    prefix: '半径：',
    baseUnit: 'cm'
>>);
```

### 2. 测量线段长度

```js
// 创建线段
seg = segment([-2, -3], [-2, 3], <<
    firstArrow: true,
    lastArrow: true
>>);

// 测量线段长度
m = measurement(1, -4, ['L', seg], <<
    prefix: '长度：',
    baseUnit: 'cm'
>>);
```

### 3. 测量滑块值

```js
// 创建滑块
slider = slider([-4, 4], [-1.5, 4], [-10, 1, 10], << name: 'a' >>);

// 测量滑块值
m = measurement(-6, -6, ['V', slider], <<
    prefix: 'm3: ',
    baseUnit: 'cm',
    dim: 1
>>);
```

### 4. 算术运算

```js
// 创建多个测量
p1 = point(1, 1);
p2 = point(1, 3);
circle = circle(p1, p2);
seg = segment([-2, -3], [-2, 3]);
slider = slider([-4, 4], [-1.5, 4], [-10, 1, 10]);

m1 = measurement(-6, -2, ['Radius', circle], <<
    prefix: 'm1: ',
    baseUnit: 'cm'
>>);

m2 = measurement(-6, -4, ['L', seg], <<
    prefix: 'm2: ',
    baseUnit: 'cm'
>>);

m3 = measurement(-6, -6, ['V', slider], <<
    prefix: 'm3: ',
    baseUnit: 'cm',
    dim: 1
>>);

// 测量值相加
m4 = measurement(2, -6,
    ['+', ['V', m1], ['V', m2], ['V', m3]], <<
    prefix: '总和：',
    baseUnit: 'cm'
>>);
```

### 5. 多种算术运算

```js
// 创建基础测量
seg1 = segment([0, 0], [3, 0]);
seg2 = segment([0, 0], [0, 4]);

m1 = measurement(1, -1, ['L', seg1], << prefix: 'a: ' >>);
m2 = measurement(1, -2, ['L', seg2], << prefix: 'b: ' >>);

// 加法
sum = measurement(1, -3,
    ['+', ['V', m1], ['V', m2]], <<
    prefix: 'a + b = '
>>);

// 减法
diff = measurement(1, -4,
    ['-', ['V', m2], ['V', m1]], <<
    prefix: 'b - a = '
>>);

// 乘法
prod = measurement(1, -5,
    ['*', ['V', m1], ['V', m2]], <<
    prefix: 'a × b = '
>>);

// 除法
quot = measurement(1, -6,
    ['/', ['V', m2], ['V', m1]], <<
    prefix: 'b ÷ a = '
>>);
```

### 6. 测量点坐标

```js
// 创建点
P = point(2, 3);

// 测量 x 坐标
mx = measurement(-2, 1, ['X', P], <<
    prefix: 'x = '
>>);

// 测量 y 坐标
my = measurement(-2, 0, ['Y', P], <<
    prefix: 'y = '
>>);
```

### 7. 带自定义单位的测量

```js
// 创建圆
circle = circle(point(0, 0), point(3, 0));

// 使用自定义单位
area = measurement(1, -2, ['Area', circle], <<
    units: <<
        dim2: '平方米'
    >>,
    prefix: '面积 = '
>>);

circumference = measurement(1, -4, ['Radius', circle], <<
    baseUnit: '米',
    prefix: '半径 = '
>>);
```

### 8. 动态更新测量

```js
// 创建可拖动的点
A = point(1, 1);
B = point(4, 5);

// 创建线段
seg = segment(A, B);

// 测量长度（会随点移动而更新）
len = measurement(2, 2, ['L', seg], <<
    prefix: '线段长度：',
    baseUnit: 'cm'
>>);

// 测量中点
mid = midpoint(A, B);
mx = measurement(2, 1, ['X', mid], << prefix: '中点 x: ' >>);
my = measurement(2, 0, ['Y', mid], << prefix: '中点 y: ' >>);
```

## 注意事项

1. **前缀表达式**：测量使用前缀表达式语法，操作符在前，操作数在后
2. **维度匹配**：测量只能与合适维度的测量组合进行运算
3. **自动更新**：当被测量的几何元素发生变化时，测量值会自动更新
4. **单位显示**：`baseUnit` 会自动添加幂次（如长度单位会自动变为面积单位的平方）
5. **坐标格式化**：当测量坐标时，需要设置 `dim: 'coords'` 并提供 `formatCoords` 函数
6. **方向格式化**：当测量方向向量时，需要设置 `dim: 'direction'` 并提供 `formatDirection` 函数
7. **显示位置**：测量值显示在指定的坐标位置，可以拖动（如果设置为可拖动）

## 相关元素

- [Text](./Text.md) - 文本元素（父类）
- [Circle](./Circle.md) - 圆（可测量面积、半径）
- [Segment](./Segment.md) - 线段（可测量长度）
- [Slider](./Slider.md) - 滑块（可测量值）
- [Point](./Point.md) - 点（可测量坐标）
