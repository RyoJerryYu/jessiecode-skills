# Segment 线段

## 描述

线段由两个端点定义。本质上是两端有限的直线（Line 元素的 `straightFirst` 和 `straightLast` 属性设为 false）。

## JessieCode 语法

```js
// 通过两个点创建线段
s = segment(A, B);

// 带固定长度的线段
s = segment(A, B, length);

// 带属性创建
s = segment(A, B) <<
    strokeColor: 'red',
    strokeWidth: 3,
    firstArrow: true,
    lastArrow: true
>>;
```

## 参数

| 参数组合 | 类型 | 描述 |
|----------|------|------|
| point1, point2 | Point/Array, Point/Array | 两个端点 |
| point1, point2, length | Point, Point, Number/Function | 两个端点加固定长度 |

## 属性

线段继承自 Line，因此拥有 Line 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `dash` | Number | 0 | 虚线样式 |
| `opacity` | Number | 1.0 | 透明度 |
| `visible` | Boolean | true | 是否可见 |
| `firstArrow` | Boolean/Object | false | 起点箭头 |
| `lastArrow` | Boolean/Object | false | 终点箭头 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `name` | String | '' | 线段名称 |

## 方法

| 方法 | 参数 | 描述 |
|------|------|------|
| `L()` | 无 | 获取线段长度 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `L(segment)` | 获取线段长度 | `L(s)` |
| `dist(P, Q)` | 计算两点距离 | `dist(A, B)` |

## 示例

### 1. 创建基本线段

```js
// 通过两个点创建
A = point(1, 1);
B = point(4, 3);
s = segment(A, B);

// 直接使用坐标
s = segment(point(0, 0), point(3, 4));
```

### 2. 设置线段样式

```js
// 红色粗线段
s1 = segment(A, B) <<
    strokeColor: 'red',
    strokeWidth: 4
>>;

// 虚线线段
s2 = segment(C, D) <<
    dash: 1,
    strokeColor: 'gray'
>>;

// 带箭头的线段（向量）
v = segment(E, F) <<
    lastArrow: true,
    strokeWidth: 3
>>;

// 双向箭头
v2 = segment(G, H) <<
    firstArrow: true,
    lastArrow: true
>>;
```

### 3. 固定长度的线段

```js
// 创建固定长度为 3 的线段
A = point(1, 1);
B = point(4, 1);
s = segment(A, B, 3);

// 使用函数定义动态长度
slider1 = slider(1, 5, 0.1);
s2 = segment(C, D, function() { return V(slider1); });

// 使用另一条线段的长度
s3 = segment(E, F, function() { return L(s); });
```

### 4. 获取线段长度

```js
A = point(0, 0);
B = point(3, 4);
s = segment(A, B);

// 使用全局函数
len1 = L(s);  // 5

// 使用元素方法
len2 = s.L();  // 5

// 使用 dist 函数
len3 = dist(A, B);  // 5
```

### 5. 线段的标签

```js
// 显示长度标签
s = segment(A, B) <<
    withLabel: true,
    name: 's'
>>;

// 自定义标签
s = segment(C, D) <<
    withLabel: true,
    name: 'AB = 5cm'
>>;
```

### 6. 三角形的边

```js
// 三角形顶点
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);

// 三边
a = segment(B, C) << strokeColor: 'red' >>;
b = segment(A, C) << strokeColor: 'blue' >>;
c = segment(A, B) << strokeColor: 'green' >>;

// 显示边长
textA = text(0, -1.5, "c = " + L(c));
textB = text(-1, 0.5, "b = " + L(b));
textC = text(1, 0.5, "a = " + L(a));
```

### 7. 动态线段

```js
// 创建可拖动的点
A = point(0, 0);
B = point(3, 0);

// 线段
s = segment(A, B);

// 显示长度
lenText = text(0, -1, "Length: " + L(s));

// 拖动 A 或 B 点时，线段长度会实时更新
```

### 8. 垂线段

```js
// 直线和外部点
l = line(point(0, 0), point(4, 0));
P = point(2, 3);

// 垂足
foot = perpendicularpoint(P, l);

// 垂线段
perpSeg = perpendicularsegment(l, P);

// 等价于
perpSeg2 = segment(P, foot);
```

### 9. 中位线

```js
// 三角形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);

// 中点
mAB = midpoint(A, B);
mBC = midpoint(B, C);
mAC = midpoint(A, C);

// 中位线
midline1 = segment(mAB, mAC);
midline2 = segment(mBC, mAB);
midline3 = segment(mAC, mBC);
```

### 10. 线段的多重变换

```js
// 原线段
A = point(1, 1);
B = point(4, 2);
s = segment(A, B);

// 创建变换
scale = transform(2, 2) << type: 'scale' >>;

// 缩放后的线段
s2 = segment(A, B, s);  // 这种方式不常用

// 更常用的方式是变换点
A2 = transform(A, scale);
B2 = transform(B, scale);
s2 = segment(A2, B2);
```

## 注意事项

1. **有限长度**：线段与直线的区别在于线段有固定长度，不会无限延伸
2. **长度可以为函数**：第三个参数可以是函数，用于创建动态长度的线段
3. **长度取绝对值**：如果长度为负数，会自动取绝对值
4. **继承 Line 属性**：线段是 Line 的特例，可以使用所有 Line 的属性

## 相关元素

- [Line](./Line.md) - 直线
- [Halfline](./Halfline.md) - 射线
- [PerpendicularSegment](./PerpendicularSegment.md) - 垂线段
- [Polygon](./Polygon.md) - 多边形（由线段组成）
