# PolePoint 极点

## 描述

极点用于创建直线关于圆锥曲线或圆的极点。极点是直线关于圆锥曲线的唯一倒数关系点。

*定义于:* [point.js](./src/src_base_point.js.md)
*继承自:* [JXG.Point](./JXG.Point.md)

## 继承关系

**[JXG.CoordsElement](./JXG.CoordsElement.md), JXG.GeometryElement**
   ↳ **[JXG.Point](./JXG.Point.md)**
      ↳ **PolePoint**

## JessieCode 语法

```js
// 创建直线关于圆锥曲线的极点
P = polepoint(conic, line);

// 创建直线关于圆的极点
P = polepoint(circle, line);

// 带属性创建
P = polepoint(c, l) <<
    strokeColor: 'red',
    size: 5,
    withLabel: true
>>;
```

## 参数

| 参数组合 | 类型 | 描述 |
|----------|------|------|
| conic, line | Conic, Line | 圆锥曲线和直线，结果为直线关于圆锥曲线的极点 |
| circle, line | Circle, Line | 圆和直线，结果为直线关于圆的极点 |
| line, conic | Line, Conic | 直线和圆锥曲线（顺序可交换） |
| line, circle | Line, Circle | 直线和圆（顺序可交换） |

**注意**：两个参数的顺序可以交换，即 `polepoint(conic, line)` 和 `polepoint(line, conic)` 效果相同

## 属性

极点继承自 Point，因此可以使用 Point 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `size` | Number | 3 | 点的大小 |
| `sizeUnit` | String | 'screen' | 大小单位：'screen' 或 'user' |
| `face` | String | 'circle' | 点的样式 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 点的名称 |
| `visible` | Boolean | true | 是否可见 |
| `fixed` | Boolean | true | 是否固定（极点通常是固定的） |

## 示例

### 1. 创建直线关于圆锥曲线的极点

```js
// 创建五个点定义圆锥曲线
p1 = point(-1, 2);
p2 = point(1, 4);
p3 = point(-1, -2);
p4 = point(0, 0);
p5 = point(4, -2);

// 创建圆锥曲线
c1 = conic(p1, p2, p3, p4, p5);

// 创建直线
p6 = point(-1, 4);
p7 = point(2, -2);
l1 = line(p6, p7);

// 创建直线关于圆锥曲线的极点
P = polepoint(c1, l1);
```

### 2. 创建直线关于圆的极点

```js
// 创建圆
p1 = point(1, 1);
p2 = point(2, 3);
c1 = circle(p1, p2);

// 创建直线
p3 = point(-1, 4);
p4 = point(4, -1);
l1 = line(p3, p4);

// 创建直线关于圆的极点
P = polepoint(c1, l1);
```

### 3. 设置极点的样式

```js
// 创建圆锥曲线
p1 = point(-2, 2);
p2 = point(2, 2);
p3 = point(3, 0);
p4 = point(0, -3);
p5 = point(-3, 0);
c1 = conic(p1, p2, p3, p4, p5);

// 创建直线
l1 = line(point(-4, 0), point(4, 0));

// 创建带样式的极点
P = polepoint(c1, l1) <<
    strokeColor: 'red',
    fillColor: 'yellow',
    size: 6,
    face: '[]',
    withLabel: true,
    name: 'P'
>>;
```

### 4. 参数顺序交换

```js
// 创建圆和直线
c1 = circle(point(0, 0), 3);
l1 = line(point(-2, 1), point(2, 1));

// 两种写法效果相同
P1 = polepoint(c1, l1);
P2 = polepoint(l1, c1);  // 与 P1 是同一点
```

### 5. 动态极点和包络线

```js
// 创建圆
c1 = circle(point(0, 0), 2);

// 创建滑块
t = slider(0, 2*PI, 0.01);

// 创建动点和切线
P = point(function() { return 3 * cos(V(t)); },
          function() { return 3 * sin(V(t)); });

// 从 P 点向圆引切线（简化示例，实际切线构造更复杂）
l1 = line(P, point(0, 0));  // 仅作为示例

// 极点在圆锥曲线上移动
Pole = polepoint(c1, l1);
```

## 极点与极线的几何关系

### 基本概念

在圆锥曲线的配极理论中：
- **极点**：平面上的一个点
- **极线**：对应于极点的一条直线

### 性质

1. **点在线上的充要条件**：如果点 P 在点 Q 的极线上，则点 Q 在点 P 的极线上
2. **切点弦**：如果从点 P 可以作圆锥曲线的两条切线，切点分别为 A 和 B，则直线 AB 就是点 P 的极线
3. **圆的极点**：对于圆心为 O、半径为 r 的圆，点 P 的极线是垂直于 OP 的直线，且满足 OP × OQ = r²（Q 为极线与 OP 的交点）

## 注意事项

1. **存在性**：不是所有直线关于圆锥曲线都有极点。当直线通过圆锥曲线的中心时（对于椭圆和双曲线），不存在极点
2. **唯一性**：在非退化情况下，直线关于圆锥曲线或圆的极点是唯一的
3. **参数顺序**：polepoint 的两个参数（圆锥曲线/圆和直线）顺序可以交换
4. **构造限制**：此元素没有直接构造函数，必须使用 `board.create()` 方法或 JessieCode 的 `polepoint()` 函数创建
5. **与圆的关系**：圆是特殊的圆锥曲线，因此 polepoint 对圆同样适用

## 相关元素

- [Point](./Point.md) - 点
- [Line](./Line.md) - 直线
- [Conic](./Conic.md) - 圆锥曲线
- [Circle](./Circle.md) - 圆
- [Tangent](./Tangent.md) - 切线
