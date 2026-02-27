# Hatch 刻度标记

<!-- USAGE_FREQUENCY: advanced -->

## 描述

刻度标记是一组短线段，用于标记全等的线段或曲线。

*定义于：* [ticks.js](./src/src_base_ticks.js.md)
*继承自：* [JXG.Ticks](./JXG.Ticks.md)

## 继承关系

**[JXG.GeometryElement](./JXG.GeometryElement.md)**
   ↳ **[JXG.Ticks](./JXG.Ticks.md)**
         ↳ **Hatch**

## JessieCode 语法

```js
// 基本语法 - 在直线上创建刻度标记
h = hatch(line, number);

// 带属性创建
h = hatch(line, 3) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    ticksDistance: 0.4,
    anchor: 0.2
>>;

// 不同的刻度样式
h = hatch(line, 2) <<
    face: '|',
    tickEndings: [1, 1]
>>;
```

## 参数

### 父元素组合

| 参数 | 类型 | 描述 |
|------|------|------|
| line | Line/Curve | 刻度标记要附着的直线或曲线 |
| numberofhashes | Number | 刻度标记的数量。刻度之间的距离可以通过 `ticksDistance` 属性控制 |

### Throws

- 如果无法使用给定的父对象构造该元素，将抛出异常

## 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `ticksDistance` | Number | 0.2 | 两个刻度符号之间的默认距离（用户坐标，非像素） |
| `anchor` | Number | 0.5 | 刻度标记在直线上的位置偏移 (0-1) |
| `face` | String | '|' | 刻度标记的样式 |
| `tickEndings` | Array | [1, 1] | 刻度线两端的延伸长度 |

### 刻度样式 (face)

| 输入值 | 外观 |
|--------|------|
| `|` | 垂直刻度线（默认） |
| `>` | 向右箭头 |
| `<` | 向左箭头 |

## 方法

继承自 [JXG.Ticks](./JXG.Ticks.md) 和 [JXG.GeometryElement](./JXG.GeometryElement.md)

## 示例

### 1. 创建基本刻度标记

```js
// 创建一条直线并添加刻度标记
p1 = point(0, 3);
p2 = point(1, 3);
l1 = line(p1, p2);
h = hatch(l1, 3);  // 3 个刻度标记
```

### 2. 调整刻度标记的位置

```js
// 创建直线
p = point(-5, 0);
q = point(5, 0);
li = line(p, q);

// 创建刻度标记，调整位置和间距
h = hatch(li, 2) <<
    anchor: 0.2,
    ticksDistance: 0.4
>>;
```

### 3. 不同的刻度样式

```js
// 创建一条斜线
li = line([-6, 0], [6, 3]);

// 垂直刻度线
h1 = hatch(li, 2) <<
    tickEndings: [1, 1],
    face: '|'
>>;

// 向右箭头，位置偏移
h2 = hatch(li, 2) <<
    tickEndings: [1, 1],
    face: '>',
    anchor: 0.3
>>;

// 向左箭头，位置偏移
h3 = hatch(li, 2) <<
    tickEndings: [1, 1],
    face: '<',
    anchor: 0.7
>>;
```

### 4. 设置刻度标记样式

```js
// 创建带样式的刻度标记
A = point(0, 0);
B = point(4, 0);
l = line(A, B);

// 红色粗刻度线
h1 = hatch(l, 3) <<
    strokeColor: 'red',
    strokeWidth: 3,
    ticksDistance: 0.5
>>;

// 蓝色刻度线，不同间距
h2 = hatch(l, 4) <<
    strokeColor: 'blue',
    ticksDistance: 0.3,
    anchor: 0.5
>>;
```

### 5. 在曲线上使用刻度标记

```js
// 创建一条曲线
c = curve(t, [sin(t), cos(2*t)], 0, 2*pi);

// 在曲线上添加刻度标记
h = hatch(c, 5) <<
    ticksDistance: 0.5
>>;
```

### 6. 标记全等线段

```js
// 创建三角形
A = point(0, 0);
B = point(4, 0);
C = point(2, 3);

a = segment(B, C);
b = segment(A, C);
c = segment(A, B);

// 标记全等边
h1 = hatch(a, 2) << ticksDistance: 0.3 >>;
h2 = hatch(b, 2) << ticksDistance: 0.3 >>;
```

## 注意事项

1. **刻度距离**：`ticksDistance` 使用用户坐标而非像素，根据图形的缩放比例调整
2. **锚点位置**：`anchor` 属性控制刻度标记在直线上的横向位置，范围 0-1，0.5 为居中
3. **父元素类型**：可以是直线 (Line) 或曲线 (Curve)
4. **刻度数量**：通过第二个参数指定刻度标记的数量
5. **样式选择**：使用 `face` 属性选择不同的刻度样式（垂直线或箭头）

## 相关元素

- [Line](./Line.md) - 直线
- [Curve](./Curve.md) - 曲线
- [Segment](./Segment.md) - 线段
- [Ticks](./Ticks.md) - 刻度
