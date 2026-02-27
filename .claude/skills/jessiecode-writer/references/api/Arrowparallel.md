# Arrowparallel 平行箭头

<!-- USAGE_FREQUENCY: advanced -->

## 描述

平行箭头是一种带箭头的线段，它平行于给定的线段。箭头从给定点出发，方向与参考线段相同。

## JessieCode 语法

```js
// 通过三点创建平行箭头
arr = arrowparallel(point1, point2, point3);

// 带属性创建
arr = arrowparallel(p1, p2, p3) <<
    strokeColor: 'blue',
    strokeWidth: 2,
    lastArrow: true
>>;
```

## 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| point1 | Point | 定义参考线段的第一个点 |
| point2 | Point | 定义参考线段的第二个点 |
| point3 | Point | 平行箭头的起点 |

## 属性

平行箭头继承自 Parallel 和 Line，因此拥有 Line 的所有属性：

| 属性 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `strokeColor` | String | '#000000' | 描边颜色 |
| `strokeWidth` | Number | 3 | 线宽 |
| `lastArrow` | Boolean | true | 末端是否显示箭头 |
| `firstArrow` | Boolean | false | 始端是否显示箭头 |
| `dash` | Number | 0 | 虚线样式 |
| `visible` | Boolean | true | 是否可见 |
| `straightFirst` | Boolean | false | 是否向前延伸 |
| `straightLast` | Boolean | false | 是否向后延伸 |

## 示例

### 1. 创建基本平行箭头

```js
// 参考线段
p1 = point(0, 2);
p2 = point(2, 1);
seg = segment(p1, p2);

// 箭头起点
p3 = point(3, 3);

// 平行箭头
arr = arrowparallel(p1, p2, p3);
```

### 2. 带样式的平行箭头

```js
// 参考线段
A = point(-2, 0);
B = point(2, 0);
seg = segment(A, B) << strokeWidth: 3 >>;

// 平行箭头 - 红色，较粗
arr = arrowparallel(A, B, point(0, 2)) <<
    strokeColor: 'red',
    strokeWidth: 3,
    lastArrow: true
>>;
```

### 3. 向量平移演示

```js
// 原始向量
A = point(0, 0);
B = point(2, 1);
vec1 = arrowparallel(A, B, A) <<
    strokeColor: 'blue',
    strokeWidth: 3
>>;

// 平移后的向量（起点不同，方向相同）
P = point(1, 2);
vec2 = arrowparallel(A, B, P) <<
    strokeColor: 'green',
    strokeWidth: 3
>>;

// 标注
text(0.5, -0.5, "Vector 1") << fontSize: 12 >>;
text(1.5, 2.5, "Vector 2 (translated)") << fontSize: 12 >>;
```

### 4. 平行四边形中的向量

```js
// 平行四边形的三个顶点
A = point(-2, -1);
B = point(2, -1);
C = point(1, 2);

// 边
AB = segment(A, B);
AC = segment(A, C);

// 对角顶点
D = point(5, 2);

// 用箭头表示向量
vecAB = arrowparallel(A, B, C) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

vecCD = arrowparallel(A, B, D) <<
    strokeColor: 'red',
    strokeWidth: 2,
    lastArrow: false,
    firstArrow: true
>>;
```

### 5. 力的分解演示

```js
// 原点
O = point(0, 0);

// 斜向的力向量
F = point(3, 2);
forceVec = arrowparallel(O, F, O) <<
    strokeColor: 'black',
    strokeWidth: 3
>>;

// 水平分力
xF = point(3, 0);
forceX = arrowparallel(O, xF, O) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 垂直分力
yF = point(0, 2);
forceY = arrowparallel(O, yF, O) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

// 辅助线（虚线）
dashLine1 = arrowparallel(O, yF, xF) <<
    strokeColor: 'gray',
    strokeWidth: 1,
    dash: 2,
    lastArrow: false
>>;

dashLine2 = arrowparallel(O, xF, yF) <<
    strokeColor: 'gray',
    strokeWidth: 1,
    dash: 2,
    lastArrow: false
>>;
```

### 6. 动态平行箭头

```js
// 可移动的参考点
A = point(0, 0);
B = point(2, 0);

// 可移动的箭头起点
P = point(1, 2);

// 动态平行箭头
arr = arrowparallel(A, B, P) <<
    strokeColor: 'blue',
    strokeWidth: 2
>>;

// 显示斜率信息
infoText = text(-3, 4, function() {
    var dx = B.X() - A.X();
    var dy = B.Y() - A.Y();
    return "Slope: " + (dy/dx).toFixed(2);
});
```

### 7. 向量场

```js
// 基础向量方向
A = point(0, 0);
B = point(0.5, 0.3);

// 在网格点上创建多个平行箭头（表示均匀向量场）
for (i = -3; i <= 3; i = i + 1) {
    for (j = -3; j <= 3; j = j + 1) {
        Pi = point(i, j);
        arrowparallel(A, B, Pi) <<
            strokeColor: 'blue',
            strokeWidth: 1
        >>;
    }
}
```

### 8. 几何变换 - 平移

```js
// 原始三角形
A = point(-2, 0);
B = point(0, -1);
C = point(0, 1);
tri1 = polygon(A, B, C) <<
    fillColor: 'lightblue',
    fillOpacity: 0.5
>>;

// 平移向量
T = point(3, 2);
transVec = arrowparallel(point(0,0), T, point(0,0)) <<
    strokeColor: 'red',
    strokeWidth: 2
>>;

// 平移后的三角形
A2 = point(A.X() + T.X(), A.Y() + T.Y());
B2 = point(B.X() + T.X(), B.Y() + T.Y());
C2 = point(C.X() + T.X(), C.Y() + T.Y());
tri2 = polygon(A2, B2, C2) <<
    fillColor: 'lightgreen',
    fillOpacity: 0.5
>>;

// 连接对应顶点的向量
arrA = arrowparallel(point(0,0), T, A) <<
    strokeColor: 'gray',
    strokeWidth: 1,
    dash: 1
>>;

arrB = arrowparallel(point(0,0), T, B) <<
    strokeColor: 'gray',
    strokeWidth: 1,
    dash: 1
>>;

arrC = arrowparallel(point(0,0), T, C) <<
    strokeColor: 'gray',
    strokeWidth: 1,
    dash: 1
>>;
```

## 注意事项

1. **方向一致性**：平行箭头的方向由 point1 到 point2 的方向决定
2. **线段模式**：与 Parallel 不同，Arrowparallel 默认显示为线段（带箭头），不会无限延伸
3. **箭头样式**：使用 `lastArrow: true` 在末端显示箭头，`firstArrow: true` 在始端显示箭头
4. **向量应用**：平行箭头非常适合用于表示向量，因为它既有方向又有大小
5. **继承关系**：Arrowparallel 继承自 Parallel，因此具有 Parallel 的所有特性

## 相关元素

- [Parallel](./Parallel.md) - 平行线
- [Segment](./Segment.md) - 线段
- [Line](./Line.md) - 直线
- [Point](./Point.md) - 点
- [Transformation](./Transformation.md) - 变换
