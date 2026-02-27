# PolarLine 极线

<!-- USAGE_FREQUENCY: advanced -->

## 描述

点的极线是点关于圆锥曲线或圆的唯一 reciprocal 关系（配极关系）。

**继承关系：**

- **JXG.GeometryElement** → **JXG.Line** → **PolarLine**

## JessieCode 语法

```js
// 通过圆锥曲线（或圆）和点创建极线
pl = polarline(conic, point);

// 也可以通过点和圆锥曲线创建（顺序可交换）
pl = polarline(point, conic);

// 带属性创建
pl = polarline(c, P) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    dash: 1
>>;
```

## 参数

| 参数组合 | 类型 | 描述 |
|----------|------|------|
| conic, point | Conic/Circle, Point | 圆锥曲线（或圆）和点 |
| point, conic | Point, Conic/Circle | 点和圆锥曲线（或圆） |

**说明：** 两种参数顺序都可以，结果都是创建点关于圆锥曲线（或圆）的极线。

## 属性

PolarLine 继承自 Line，因此可以使用 Line 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽（像素） |
| `dash` | Number | 0 | 虚线样式：0=实线，1=虚线，2=点线，3=点划线 |
| `opacity` | Number | 1.0 | 透明度 (0-1) |
| `visible` | Boolean | true | 是否可见 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 极线名称 |

## 示例

### 1. 点关于圆锥曲线的极线

```js
// 定义圆锥曲线上的五个点
p1 = point(-1, 2);
p2 = point(1, 4);
p3 = point(-1, -2);
p4 = point(0, 0);
p5 = point(4, -2);

// 创建圆锥曲线
c1 = conic(p1, p2, p3, p4, p5);

// 创建另一个点
p6 = point(-1, 1);

// 创建点 p6 关于圆锥曲线 c1 的极线
pl = polarline(c1, p6);
```

### 2. 点关于圆的极线

```js
// 创建圆（通过圆心和圆周上的点）
center = point(1, 1);
radiusPoint = point(2, 3);
c1 = circle(center, radiusPoint);

// 创建外部点
p3 = point(6, 6);

// 创建点 p3 关于圆 c1 的极线
pl = polarline(c1, p3);
```

### 3. 设置极线样式

```js
// 定义圆锥曲线
p1 = point(-1, 2);
p2 = point(1, 4);
p3 = point(-1, -2);
p4 = point(0, 0);
p5 = point(4, -2);
c1 = conic(p1, p2, p3, p4, p5);

// 创建带样式的极线
p6 = point(-1, 1);
pl = polarline(c1, p6) <<
    strokeColor: 'red',
    strokeWidth: 3,
    dash: 1,
    withLabel: true,
    name: '极线'
>>;
```

### 4. 参数顺序可交换

```js
// 创建圆
c1 = circle(point(0, 0), 2);

// 创建点
P = point(3, 3);

// 两种写法效果相同
pl1 = polarline(c1, P);
pl2 = polarline(P, c1);
```

### 5. 动态极线

```js
// 创建圆
c1 = circle(point(0, 0), 2);

// 创建可拖动的点
P = point(3, 0);

// 创建极线 - 当 P 点移动时，极线会动态更新
pl = polarline(c1, P) <<
    strokeColor: 'blue'
>>;
```

## 注意事项

1. **无直接构造函数**：在 JessieCode 中使用 `polarline(conic, point)` 函数创建
2. **参数顺序可交换**：圆锥曲线和点的顺序可以互换，结果相同
3. **支持圆锥曲线和圆**：可以用于任意圆锥曲线（椭圆、双曲线、抛物线）或圆
4. **几何意义**：
   - 当点在圆锥曲线外部时，极线是通过该点作圆锥曲线的两条切线的切点连线
   - 当点在圆锥曲线上时，极线就是该点的切线
   - 当点在圆锥曲线内部时，极线在圆锥曲线外部
5. **继承 Line 属性**：作为 Line 的子类，可以使用所有 Line 的属性，如 `dash`、`strokeWidth` 等

## 相关元素

- [Line](./Line.md) - 直线
- [Conic](./Conic.md) - 圆锥曲线
- [Circle](./Circle.md) - 圆
- [Tangent](./Tangent.md) - 切线
