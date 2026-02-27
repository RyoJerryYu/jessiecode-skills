# Midpoint 中点

## 描述

中点是两个点或一条线段的中点。中点的坐标是两个端点坐标的平均值。

## JessieCode 语法

```js
// 通过两个点创建中点
M = midpoint(A, B);

// 通过线段创建中点
M = midpoint(segment1);

// 带属性创建
M = midpoint(A, B) <<
    strokeColor: 'red',
    size: 5,
    withLabel: true
>>;
```

## 参数

### 方式一：两个点

| 参数 | 类型 | 描述 |
|------|------|------|
| p1 | Point | 第一个点 |
| p2 | Point | 第二个点 |

### 方式二：一条线段

| 参数 | 类型 | 描述 |
|------|------|------|
| line | Line/Segment | 线段（使用中点） |

## 属性

中点继承自 Point，因此拥有 Point 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `fillColor` | String | '#ffffff' | 填充颜色 |
| `size` | Number | 3 | 点的大小 |
| `face` | String | 'circle' | 点的样式 |
| `withLabel` | Boolean | false | 是否显示标签 |
| `visible` | Boolean | true | 是否可见 |

## 方法

中点继承自 Point，拥有 Point 的所有方法：

| 方法 | 描述 |
|------|------|
| `X()` | 获取 x 坐标 |
| `Y()` | 获取 y 坐标 |

## 全局函数

| 函数 | 描述 | 示例 |
|------|------|------|
| `midpoint(A, B)` | 计算中点坐标 | `midpoint(A, B)` |

## 示例

### 1. 创建基本中点

```js
// 两个点
A = point(-2, 0);
B = point(2, 0);

// 中点
M = midpoint(A, B);

// 标记中点
M = midpoint(A, B) <<
    strokeColor: 'red',
    fillColor: 'black',
    size: 5,
    face: '[]'
>>;
```

### 2. 线段的中点

```js
// 创建线段
A = point(1, 1);
B = point(5, 3);
s = segment(A, B);

// 线段的中点
M = midpoint(s);

// 显示中点坐标
text(1, 4, "Midpoint: (" + M.X().toFixed(2) + ", " + M.Y().toFixed(2) + ")");
```

### 3. 三角形的中线

```js
// 三角形
A = point(-2, -1);
B = point(2, -1);
C = point(0, 2);
pol = polygon(A, B, C);

// 各边中点
mAB = midpoint(A, B);
mBC = midpoint(B, C);
mAC = midpoint(A, C);

// 中线
medianA = segment(A, mBC);
medianB = segment(B, mAC);
medianC = segment(C, mAB);

// 重心（中线交点）
centroid = intersection(medianA, medianB, 0);
```

### 4. 中点四边形

```js
// 任意四边形
A = point(-3, -2);
B = point(3, -1);
C = point(2, 2);
D = point(-2, 3);
quad = polygon(A, B, C, D);

// 各边中点
mAB = midpoint(A, B);
mBC = midpoint(B, C);
mCD = midpoint(C, D);
mDA = midpoint(D, A);

// 中点四边形（总是平行四边形）
varignon = polygon(mAB, mBC, mCD, mDA) <<
    fillColor: 'lightblue',
    fillOpacity: 0.5
>>;
```

### 5. 动态中点

```js
// 可拖动的点
A = point(-2, 0);
B = point(2, 0);

// 动态中点
M = midpoint(A, B);

// 显示距离
distText = text(0, 1, function() {
    return "AM = " + dist(A, M).toFixed(2);
});
```

### 6. 垂直平分线

```js
// 线段
A = point(-2, -1);
B = point(2, 1);
s = segment(A, B);

// 中点
M = midpoint(A, B);

// 垂直平分线
perpBisector = perpendicular(s, M);

// 验证：垂直平分线上的点到 A 和 B 等距
P = glider(perpBisector);
text(0, 3, function() {
    return "PA = " + dist(P, A).toFixed(2) + ", PB = " + dist(P, B).toFixed(2);
});
```

### 7. 中位线定理

```js
// 三角形
A = point(-3, -2);
B = point(3, -1);
C = point(0, 3);
pol = polygon(A, B, C);

// 两边中点
mAB = midpoint(A, B);
mAC = midpoint(A, C);

// 中位线
midline = segment(mAB, mAC);

// 验证中位线定理
text(-3, 4, function() {
    return "BC = " + dist(B, C).toFixed(2);
});
text(-3, 3.5, function() {
    return "Midline = " + dist(mAB, mAC).toFixed(2);
});
// 中位线长度 = 底边长度的一半
```

### 8. 中点坐标公式演示

```js
// 两个点
A = point(-4, -2);
B = point(4, 2);

// 中点
M = midpoint(A, B);

// 显示坐标公式
formulaText = text(-4, 3, "M = ((" + A.X() + "+" + B.X() + ")/2, (" + A.Y() + "+" + B.Y() + ")/2)");
resultText = text(-4, 2.5, "M = (" + M.X() + ", " + M.Y() + ")");
```

### 9. 多个中点的组合

```js
// 创建点列
A = point(-4, 0);
B = point(4, 0);

// 递归中点
M1 = midpoint(A, B);
M2 = midpoint(A, M1);
M3 = midpoint(M1, B);
M4 = midpoint(A, M2);
M5 = midpoint(M2, M1);
M6 = midpoint(M1, M3);
M7 = midpoint(M3, B);

// 所有中点用相同样式
points = [M1, M2, M3, M4, M5, M6, M7];
// 可以通过循环设置样式
```

### 10. 中点与圆的组合

```js
// 线段（直径）
A = point(-2, 0);
B = point(2, 0);
s = segment(A, B);

// 中点（圆心）
O = midpoint(A, B);

// 圆（以 AB 为直径）
c = circle(O, A);

// 圆上任意点
P = glider(c);

// 角 APB 是直角（泰勒斯定理）
angleAPB = angle(A, P, B) <<
    radius: 0.5,
    type: 'square'
>>;
```

## 注意事项

1. **动态更新**：当端点移动时，中点会自动更新位置
2. **线段中点**：可以通过线段创建中点，等价于通过线段的两个端点创建
3. **继承属性**：中点继承自 Point，可以使用所有 Point 的属性和方法
4. **数值精度**：对于非常远或非常近的点，可能存在数值精度问题

## 相关元素

- [Point](./Point.md) - 点
- [Segment](./Segment.md) - 线段
- [Intersection](./Intersection.md) - 交点
- [Glider](./Glider.md) - 滑点
