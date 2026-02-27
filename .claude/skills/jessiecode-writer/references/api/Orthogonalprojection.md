# Orthogonalprojection 正交投影点

<!-- USAGE_FREQUENCY: common -->

## 描述

正交投影点是将一个点垂直投影到一条直线上得到的点。该点位于直线上，且连接原点与投影点的线段与直线垂直。

## JessieCode 语法

```js
// 基本语法 - 创建点在直线上的正交投影
P = orthogonalprojection(point, line);

// 带属性创建
P = orthogonalprojection(A, l) <<
    strokeColor: 'red',
    fillColor: 'yellow',
    size: 5,
    withLabel: true,
    name: 'P'
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| point | Point | 要进行投影的点 |
| line | Line | 目标直线（点将投影到此直线上） |

## 属性

正交投影点继承自 `Point` 元素，因此支持所有点的属性。

### 常用属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `size` | Number | 3 | 点的大小（像素或用户坐标） |
| `sizeUnit` | String | 'screen' | 大小单位：'screen' 或 'user' |
| `face` | String | 'circle' | 点的样式 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 点的名称 |
| `id` | String | 自动生成 | 元素的唯一 ID |
| `visible` | Boolean | true | 是否可见 |
| `fixed` | Boolean | true | 是否固定（投影点默认固定，不可拖动） |
| `showInfobox` | Boolean | true | 是否显示信息框 |

## 方法

正交投影点继承自 `Point` 元素，因此支持所有点的方法。

| 方法 | 参数 | 描述 |
|------|------|------|
| `X()` | 无 | 获取 x 坐标 |
| `Y()` | 无 | 获取 y 坐标 |
| `move(dx, dy)` | dx, dy: Number | 移动点（投影点通常不可移动） |
| `glide(line)` | line: Line | 使点在直线上滑动 |
| `free()` | 无 | 释放点 |

## 示例

### 1. 创建基本正交投影点

```js
// 创建两个点定义一条直线
p1 = point(0.0, 4.0);
p2 = point(6.0, 1.0);

// 创建直线
l1 = line(p1, p2);

// 创建要投影的点
p3 = point(3.0, 3.0);

// 创建 p3 在直线 l1 上的正交投影点
pp1 = orthogonalprojection(p3, l1);
```

### 2. 设置投影点的样式

```js
// 创建直线
A = point(0, 0);
B = point(5, 3);
l = line(A, B);

// 创建要投影的点
P = point(2, 4) <<
    strokeColor: 'blue',
    fillColor: 'lightblue',
    size: 6
>>;

// 创建红色的投影点
proj = orthogonalprojection(P, l) <<
    strokeColor: 'red',
    fillColor: 'yellow',
    size: 8,
    face: 'square',
    withLabel: true,
    name: 'P\''
>>;
```

### 3. 动态投影点

```js
// 创建可拖动的点
A = point(0, 0);
B = point(4, 0);
l = line(A, B);

// 创建可拖动的投影源点
P = point(2, 3);

// 创建投影点（随 P 的移动而自动更新）
proj = orthogonalprojection(P, l);

// 创建连接 P 和 proj 的垂线
perpLine = line(P, proj) <<
    dash: 1,
    strokeColor: 'gray'
>>;
```

### 4. 多个投影点

```js
// 创建坐标轴
xAxis = line(0, 0, 1, 0) << withLabel: true, name: 'x' >>;
yAxis = line(0, 0, 0, 1) << withLabel: true, name: 'y' >>;

// 创建任意点
P = point(3, 2);

// 创建在 x 轴和 y 轴上的投影
projX = orthogonalprojection(P, xAxis) <<
    strokeColor: 'blue',
    face: 'plus'
>>;
projY = orthogonalprojection(P, yAxis) <<
    strokeColor: 'green',
    face: 'plus'
>>;

// 创建投影辅助线
lineX = line(P, projX) << dash: 1, strokeColor: 'gray' >>;
lineY = line(P, projY) << dash: 1, strokeColor: 'gray' >>;
```

### 5. 投影点到直线的距离

```js
// 创建直线
A = point(0, 0);
B = point(5, 0);
l = line(A, B);

// 创建外部点
P = point(2, 3);

// 创建投影点
proj = orthogonalprojection(P, l);

// 计算距离（使用 dist 函数）
// 注意： JessieCode 中可以使用 dist(P, proj) 获取距离
```

### 6. 垂足三角形

```js
// 创建三角形顶点
A = point(0, 0);
B = point(5, 0);
C = point(2, 4);

// 创建三角形边
a = line(B, C);
b = line(A, C);
c = line(A, B);

// 创建高线的垂足（顶点到对边的投影）
Ha = orthogonalprojection(A, a);
Hb = orthogonalprojection(B, b);
Hc = orthogonalprojection(C, c);

// 创建垂足三角形
orthicTriangle = polygon(Ha, Hb, Hc) <<
    fillColor: 'yellow',
    opacity: 0.5
>>;
```

## 注意事项

1. **投影点位置**：正交投影点始终位于目标直线上
2. **垂直关系**：连接原点与投影点的线段与目标直线垂直
3. **固定属性**：投影点默认是固定的（`fixed: true`），不能直接拖动
4. **动态更新**：当源点或目标直线移动时，投影点会自动更新位置
5. **继承特性**：投影点继承自 Point 元素，支持点的所有属性和方法
6. **创建方式**：必须使用 `orthogonalprojection(point, line)` 语法创建

## 相关元素

- [Point](./Point.md) - 点
- [Line](./Line.md) - 直线
- [Perpendicular](./Perpendicular.md) - 垂线
- [Projection](./Projection.md) - 投影点
- [Foot](./Foot.md) - 垂足
